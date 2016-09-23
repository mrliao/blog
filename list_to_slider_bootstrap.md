```javascript
'use strict';
// 列表变成 base on bootstap
var listToSlider = function() {
        //当浏览器大小变化时
        var curWidth = $(document.body).outerWidth(true);
        if(curWidth <= 600) {
            $("body").attr("onmousewheel", "return false;");
            $.each($(".list-to-slider"), function(i, v) {
                var id =  $(v).attr('id');
                $(v).addClass('carousel slide').attr("data-ride", "carousel");
                $(v).children('div:first-child').addClass('carousel-inner').attr('role','listbox');
                $(v).children('div:first-child').children().addClass("item");
                $("#" + id + '-item-0').addClass('active');
                var controlHtml = '<a class="left carousel-control" href="#'+id+'" role="button" data-slide="prev">'
                        + '<span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>'
                        + '<span class="sr-only">Previous</span> </a>'
                        + '<a class="right carousel-control" href="#'+id+'" role="button" data-slide="next">'
                        + '<span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>'
                        + '<span class="sr-only">Next</span></a>';
                $(v).append(controlHtml);
            });
        }
    };
    listToSlider();
```
