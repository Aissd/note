防抖：关键是定时器
一般用在输入框中，防止重复输入，重复发送请求...
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>防抖</title>
</head>

<body>
    防抖或是节流：限制函数的执行次数 <br />
    1、防抖（debounce）：通过setTimeout的方式，在一定的时间间隔内，将多次触发变成一次触发； <br />
    2、节流（throttle ）：减少一段时间的触发频率； <br />
    <input type="text" id="input" />
    <input type="submit" id="btn" />
    <script>
        // ----------------------- 防抖 -----------------------
        var btn = document.getElementById('btn');

        btn.addEventListener('click', debounce(submit, 1000), false);

        function submit(e) {
            console.log(this);
            console.log(e);
        }

        // 防抖
        function debounce(fn, timer) {
            var t = null;
            return function () {
                var firstClick = !t;

                if (t) { clearTimeout(t); }

                if (firstClick) { fn.apply(this, arguments); }

                t = setTimeout(function () {
                    t = null;
                }, timer);
            }
        }

        // ----------------------- 适合click的节流 ---------------------------
        // var input = document.getElementById('input');

        // input.addEventListener('input', throttle(inputFn, 1000), false);

        // function inputFn() {
        //     console.log(input.value);
        // }

        // // 适合click的节流
        // function throttle(fn, delay) {
        //     var begin = 0;
        //     return function () {
        //         var cur = new Date().getTime();
        //         if (cur - begin > delay) {
        //             fn.apply(this, arguments);
        //             begin = cur;
        //         }
        //     }
        // }

        // ----------------------- 适合input的节流 ---------------------------
        var text = document.querySelector("input");
        text.addEventListener("input", throttle(inputFn, 500), false);

        // 适合input的节流
        function throttle(fn, timer) {
            var t1 = null;
            return function() {
                var that = this;
                if (t1) return;
                t1 = setTimeout(function(elem) {
                    fn.call(that, elem.value);
                    clearTimeout(t1);
                    t1 = null;
                }, timer, this);
            }
        }

        function inputFn(val) {
            console.log(this, val);
        }

    </script>
</body>

</html>
```