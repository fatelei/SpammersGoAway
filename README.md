# SpammersGoAway

## 阻挡原理

对于 Spammer 来说，效率是摆在第一位的。他们需要用极短的时间来发送大量的 SPAM ，这就是 Spammer 和普通的用户最显著的区别。

利用这一点，我们可以使每位评论者都花上一点点的时间来计算一个特殊的 hash 值，比如`hash(time+i)`，然后循环使`i`自增，最后要求计算出来的 hash 满足一个特殊的条件如前3位相同，这样对于一个 Spammer 来说，他发送一个 SPAM 所使用的资源提高了：需要更多的 CPU 和时间。而对于普通用户来说，浏览器计算这个 hash 值的时间在 3 秒内，还不够用户输入一条完整的评论，对于用户来说几乎无影响。

## 使用说明

在`usr/plugins/`下新建一个目录`SpammersGoAway`，将`Plugins.php`和`footer.js`放入其中，在 typecho 后台启用插件即可。

## 配置说明

### 挑战难度等级

浏览器计算 hash 时，要求前几位为特定值。此数字越大，浏览器计算耗时越长，页面响应越慢。推荐取2或3即可。

### 挑战超时

浏览器计算出的 hash 在多久内有效。建议设置一个合适的值，300~3000均可。

## 使用测试

启用并设置完成插件后，请退出登录并回到你的前台，打开任意一个文章页并打开浏览器控制台（F12），输入评论作者、邮箱、网站信息，并将光标定位到评论输入框中。稍等片刻，控制台中会出现两条以`[SpammersGoAway]`开头的信息，显示了经过多少次尝试后成功计算出了 hash ，以及计算耗时。

如果你的浏览器控制台中没有出现此信息，请不要启用插件。通常，这是由于主题不支持此插件导致的。

提交评论后，如果一切顺利，你应该可以成功的发表你的评论。如果出现错误，请对照错误代码表检查。

## 错误代码

* 错误1：无法找到提交的 hash 值。此错误通常是由于模版不支持本插件引起，请尝试更换模版。若错误不重现，请提交 issue 交由作者处理。

* 错误2：hash 的前N位不符合规则。此错误通常是由于 CPU 计算错误导致，请重试。若错误依然出现，请提交 issue 。

* 错误3：key 超时。此错误是由于后台设置的超时过短引起，请调高超时值后重试。

* 错误4：hash 校验失败。此错误出现原因与2相似，请重新尝试，并检查服务器是否支持`hash`函数。若服务器支持`hash`且错误依然出现，请提交 issue 。