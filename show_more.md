###  phpcms ajax show more
```javascript
'use strict';
var dduFunc = {currentPage: 1};
dduFunc.tplConfig = {
    newsTpl: [
        {
            author_text: "author",
            news_link_text: 'show more',
            inputtime_text: 'datetime'
        }
    ]
};
//--------------------------------------------//
// 模板
dduFunc.defaultTemplates = {
    newsTpl: function() {
        return '<li class="border-bottom-2">' +
            '<div class="col-sm-12"> ' +
            '<div class="col-sm-8 text-left"> ' +
            '<h5>#title#</h5> ' +
            '</div> ' +
            '</div> ' +
            '<p  class="text-left ddu-font-12"> <img src="#thumb#" class="img-responsive"/> ' +
            '<span class="text-left">#author_text#:#username#|#inputtime_text#:#inputtime# ' +
            '</span> </p> <p class="text-left ddu-font-12">#description#</p> ' +
            '<p class="text-right col-sm-12 ddu-font-12 ddu-color">' +
            '<a href="#url#" title="#title#">#news_link_text#&nbsp;' +
            '<img src="statics/dduwork/source/images/Arrow-Right.png" />' +
            '</a>' +
            '</p> ' +
            '</li>';
    },
    memberTpl: function() {
        return '';
    }
};
/**
 * 格式化类库
 * @param formatType
 * @returns {*}
 */
dduFunc.format = function(formatType) {
    var formatConfig = {
        dateFormat: function (timestamp) {
            var newDate = new Date();
            newDate.setTime(timestamp * 1000);
            return newDate.toTimeString()
        }
    }
    return formatConfig[formatType] === 'undefined' ? null : formatConfig[formatType];
}
//操作模版
dduFunc.opTemplate = function() {
    var self = this;
    return {
        /**
         * 增加模板
         * @param templateFlag
         * @param template
         * @returns {*}
         */
        addTpl: function(templateFlag, template) {
            if(this.hasTpl(templateFlag)) {
                return templateFlag;
            }
            self.defaultTemplates[templateFlag] = template;
        },
        /**
         * 模板key
         * @param templateFlag
         * @returns {boolean}
         */
        hasTpl: function(templateFlag) {
            if(self.defaultTemplates[templateFlag] != undefined) {
                return true;
            }
            return false;
        },
        /**
         * 获取模板内容
         * @param templateFlag
         * @returns {*}
         */
        getTpl: function(templateFlag) {
            return self.defaultTemplates[templateFlag]();
        },
        /**
         * 移除模板
         * @param templateFlag
         */
        removeTpl: function(templateFlag) {
            delete self.defaultTemplates[templateFlag];
        },
        /**
         * 替换模版
         * @param data
         * @param template
         * @returns {*}
         */
        replaceTpl: function(data, template) {
            var tplHtml = [];
            $.each(data, function( i, v ) {
                var initTpl = template;
                $.each(v, function( field, value ) {
                    var re =new RegExp("#" + field + "#");
                    initTpl = initTpl.replace(re, value);
                });
                tplHtml.push(initTpl);
            });
            return tplHtml.join();
        }
    }
}
/**
 * 获取更多
 * @param appendId 追加内容的id
 * @param fetchUrl 获取数据的url
 * @param templateFlag 模板key
 * @param template 展示模版
 */
dduFunc.getMoreList = function(obj, appendId, fetchUrl, templateFlag, template) {
    var self = this;
    var op = self.opTemplate();
    if(!template && templateFlag && op.hasTpl(templateFlag)) template = op.getTpl(templateFlag);
    // 模板解析
    var templatePattern = self.tplConfig[templateFlag];
    // showloading
    $.post(fetchUrl + '&page=' + self.currentPage, function(res) {
        if(res.status === 0 && res.data.length) {
            // config replace
            template = op.replaceTpl(templatePattern, template);
            var html = op.replaceTpl(res.data, template);
            $('#' + appendId).append(html);
            self.currentPage++;
        } else {
            $(obj).html(' no more ');
        }
    });
}
;

```

### php api
```php
header('Content-Type:application/json; charset=utf-8');
// model 配置
$tag = (string)$_GET['tag'];
$page = intval($_GET['page']);
$tag_permission = [
    'content_lists' => ['catid', 'thumb']
];

if(array_key_exists($tag, $tag_permission)) {
    $cls_info = ddu_common::get_class_by_tag($tag);
    if(is_bool($cls)) {
        exit(json_encode(['data' => null, 'msg' => 'error request', 'status' => '-2']));
    }
    $permission_param = $tag_permission[$tag];
    $permit_exist = [];
    foreach($_GET as $param_key => $param) {
        if(in_array($param_key, $permission_param)) {
            $permit_exist[$param_key] = $param;
        }
    }
    if(count($permit_exist) !== count($permission_param)) {
        exit(json_encode(['data' => null, 'msg' => 'error request', 'status' => '-3']));
    }
    $data = [
        'limit' => ddu_common::get_limit($page+1),
    ];
    $data = array_merge($permit_exist, $data);
    exit(json_encode(['data' => array_values($cls_info['cls']->$cls_info['method']($data)), 'msg' => 'success', 'status' => 0]));
} else {
    exit(json_encode(['data' => null, 'msg' => 'error request', 'status' => '-1']));
}


/**
 * @param $tag
 */
class ddu_common
{
    /**
     * @param $tag
     * @return array|bool
     */
    public static function get_class_by_tag($tag)
    {
        $tag_split_arr = explode('_', $tag);
        if (count($tag_split_arr) < 2) {
            return false;
        }
        $op = $tag_split_arr[0];
        $method = $tag_split_arr[1];
        if (file_exists(PC_PATH . DIRECTORY_SEPARATOR . 'modules' . DIRECTORY_SEPARATOR . $op . DIRECTORY_SEPARATOR . 'classes' . DIRECTORY_SEPARATOR . $op . '_tag.class.php')) {
            return ['cls' => pc_base::load_app_class($op.'_tag', $op), 'method' => $method];
        } else {
            return false;
        }
    }

    /**
     * @param int $pagesize
     * @param int $page
     * @return string
     */
    public static function get_limit( $page = 1, $pagesize = 3)
    {
        return ($page-1) * $pagesize . ',' . $pagesize;
    }
}
```
