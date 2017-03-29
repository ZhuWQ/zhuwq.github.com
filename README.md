<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>http://www.zhinengshe.com/</title>
    <style>
        .box div {
            width: 200px;
            height: 200px;
            border: 1px solid #000;
            font-size: 50px;
            line-height: 200px;
            text-align: center;
            display: none;
        }
        .box input.active {
            background: #f60;
            color: #fff;
        }
    </style>
    <script>
        // 定义一个类
        class Tab {
            constructor(id) {
                this.oBox = document.getElementById(id);
                this.aBtn = this.oBox.getElementsByTagName('input');
                this.aDiv = this.oBox.getElementsByTagName('div');
                this.init();
            }
            init() {
                for (let i = 0; i < this.aBtn.length; i++) {
                    this.aBtn[i].onclick = function() {
                        this.hide(); // 清空所有
                        this.show(i);// 设置当前
                    }.bind(this);
                }
            }
            hide() {
                for (let i = 0; i < this.aBtn.length; i++) {
                    this.aBtn[i].className = '';
                    this.aDiv[i].style.display = 'none';
                }
            }
            show(index) {
                this.aBtn[index].className = 'active';
                this.aDiv[index].style.display = 'block';
            }
        }
        // 定义一个自动播放的类
        class AutoTab extends Tab {
            constructor(id,autoPlay=true){
                super(id); // 继承父级的属性 ->*** 必须写在第一句
                this.autoPlay = autoPlay;

                this.iNow = 0;
                if (autoPlay) {
                    setInterval(function() {
                        this.next();
                    }.bind(this),1000);
                }
            }
            next() {
                this.iNow++;
                if (this.iNow == this.aBtn.length) {
                    this.iNow = 0;
                }
                this.hide(); // 清空所有
                this.show(this.iNow);// 设置当前
            }
            init() {
                for (let i = 0; i < this.aBtn.length; i++) {
                    this.aBtn[i].onclick = function() {
                        this.iNow = i;
                        this.hide(); // 清空所有
                        this.show(this.iNow);// 设置当前
                    }.bind(this);
                }
            }
        }
        window.onload = () => {
            new Tab('box');
            new AutoTab('box2',true);
        };
    </script>
</head>
<body>
    <div id="box" class="box">
        <input class="active" type="button" value="热点">
        <input type="button" value="新闻">
        <input type="button" value="娱乐">
        <div style="display: block;">热点</div>
        <div>新闻</div>
        <div>娱乐</div>
    </div>
    <div id="box2" class="box">
        <input class="active" type="button" value="热点">
        <input type="button" value="新闻">
        <input type="button" value="娱乐">
        <div style="display: block;">热点</div>
        <div>新闻</div>
        <div>娱乐</div>
    </div>
</body>
</html>
