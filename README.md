# loginModal
use bootstrap and jquery to build a better login modal

## 图片以及效果
![点击按钮弹出模态框](https://github.com/GzhiYi/loginModal/blob/master/img/click%20button.png)
![点击忘记密码](https://github.com/GzhiYi/loginModal/blob/master/img/%E7%82%B9%E5%87%BB%E5%BF%98%E8%AE%B0%E5%AF%86%E7%A0%81.png)

## 引用的js情况
所使用的js文件为：
```
    <script src="js/jquery-3.1.1.min.js"></script>
    <script src="js/bootstrap.min.js"></script>
    <script src="js/jquery.metadata.js"></script>
    <script src="js/jquery.validate.min.js"></script>
    <script src="js/messages_zh.min.js"></script>
    <font color=#0099ff><script src="js/login.js"></script></font>
```
 省略几个js文件，关于页面js为文件 login.js 。文件已经上传到git
 
 ## 代码注释
 1. 表单bootstrap代码不说明，很容易。表单里边有php代码不影响阅读但是没有php环境在表单会直接显示value值，也就是一段php代码。
 2. 说明login.js文件：
    validate中messages解释
    ```
    //为validate验证增加bootstrap提示，如class has-error的add和remove
    <font color=#0099ff></script></font>
    highlight: function(element) {
        $(element).closest('.form-group').addClass('has-error');
    },
    unhighlight: function(element) {
        $(element).closest('.form-group').removeClass('has-error');
    },
    errorElement: 'span',
    errorClass: 'help-block',
    //解决bootstrap中input-group和表单验证validate的问题，也就是表单验证error会将一个input框和button分隔开。
    errorPlacement: function(error, element) {
        if(element.parent('.input-group').length) {
            error.insertAfter(element.parent());
        } else {
            error.insertAfter(element);
        }
    }
     ```
     
     主要脚本解释:
     ```
     $(function() {
        $('#forget_pwd').click(function() {
            $('#resForm').load("forget_pwd.html #forget_pwd");//异步加载forget_pwd.html 中的#forget_pwd
            $('#form-outer *').attr("disabled",true);
            $("#login_title").html("找回密码");
            $("#a_reg").css("pointer-events","none");
        });
        //找回密码输入邮箱处的validate验证
        $('#form_forget_pwd').validate({
            rules: {
                forget_pwd_email: {
                    required: true,
                    email: true
                }
            }
        })
    });
    $(function() {//这个模态框隐藏后触发，关闭resForm内容，起到重置的作用
        $('.modal').on('hidden.bs.modal', function(e)
        {
            $("#resForm").html("");
            $('#form-outer *').attr("disabled",false);
            $("#login h4").html("用户登录");
        }) ;
    })
    ```

 
