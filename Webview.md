# Webview



## 1.透明背景

* webview.setbackground(Color.TRANSPARENT);

可能会出现闪屏，需要关闭硬件加速，关闭方法：

`webview.setLayerType(WebView.LAYER_TYPE_SOFTWARE, null);`

* webview.setbackground(0x01000000);

同样可以实现透明效果

