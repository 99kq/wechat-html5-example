# wechat-html5-example 

微信分享页面模版
---## 模块1. 初始模板2. 基础JS模块3. 微信JSSDK4. 代码规范 ## 初始模板package.json    {      "name": "youproject",      "version": "0.0.1",      "description": "project description",      "scripts": {    "start": "node node_modules/gulp/bin/gulp"      },      "dependencies": {},      "devDependencies": {	    "bower": "^1.3.3",	    "gulp": "~3.8.10",	    "gulp-concat": "~2.4.1",	    "gulp-connect": "^2.2.0",	    "gulp-jade": "~0.10.0",	    "gulp-minify-css": "~0.3.11",	    "gulp-rename": "~1.2.0",	    "gulp-stylus": "~1.3.4",	    "gulp-util": "^2.2.14",	    "gulp-watch": "~1.1.0",	    "shelljs": "^0.3.0"      }    }gulpfile.jsjavascript libcssindex.html## 基础JS模板### Loading### Page info### 统计埋点### REM方案布局相应* Html    <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no"/    * Style      html {font-size:50px;}* JavaScript        /* javascript */

        -[1, ] || (function() {

        //为window对象添加

        addEventListener = function(n, f) {
            if ("on" + n in this.constructor.prototype)
                this.attachEvent("on" + n, f);
            else {
                var o = this.customEvents = this.customEvents || {};
                n in o ? o[n].push(f) : (o[n] = [f]);
            };
        };
        removeEventListener = function(n, f) {
            if ("on" + n in this.constructor.prototype)
                this.detachEvent("on" + n, f);
            else {
                var s = this.customEvents && this.customEvents[n];
                if (s)
                    for (var i = 0; i < s.length; i++)
                        if (s[i] == f) return void s.splice(i, 1);
            };
        };
        dispatchEvent = function(e) {
            if ("on" + e.type in this.constructor.prototype)
                this.fireEvent("on" + e.type, e);
            else {
                var s = this.customEvents && this.customEvents[e.type];

                if (s)
                    for (var s = s.slice(0), i = 0; i < s.length; i++)

                s[i].call(this, e);

            }

        };

        })();

        !(function(win, doc) {

        function setFontSize() {

            var winWidth = doc.documentElement.clientWidth;

            if (winWidth <= 479) {

                doc.documentElement.style.fontSize = (winWidth / 640) * 100 + 'px';

            } else {

                doc.documentElement.style.fontSize = '12px';

            }

        }

        var evt = 'onorientationchange' in win ? 'orientationchange' : 'resize';

        var timer = null;

        win.addEventListener(evt, function() {
            clearTimeout(timer);

            timer = setTimeout(setFontSize, 300);
        }, false);

        win.addEventListener("pageshow", function(e) {
            if (e.persisted) {
                clearTimeout(timer);

                timer = setTimeout(setFontSize, 300);
            }
        }, false);

        // 初始化
        setFontSize();

    }(window, document));
#### 页面元素尺寸例如设计稿页面宽度640PX：元素300PX =》 30rem#### 页面字体尺寸绑定元素的文字，需要使用REM尺寸和排版无关的文字，最小需要12PX，加大字体另计。## 微信JSSDK模块### 硬写分享链接### SDK分享基本配置### 微信分享JS设置### 无JSSDK时的调整## 代码规范### 参考规范### 合并文件
