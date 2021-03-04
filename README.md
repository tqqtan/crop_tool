# Clipping

#### 介绍
网页端的图片裁剪组件（原生JS、无依赖）

#### 使用说明 CDN

```
<script src="croptool.min.js"></script>
<script>
    window.clip = new Clip({
        dragBoxClass: 'block',  //裁剪框类名 
        clipRadio: 4 / 3,       //裁剪比例 传0或空或不传等于不设置比例
        cornerColor: '#f00',    //剪裁框颜色 默认#39f,
        maxWidth: 300,
        //图片文件
        encode: 'base64',       //支持 base64、blob、file
        type: 'png',            //保存类型
        name: 'rtest',          //文件名称
        quality: 0.9,           //导出图片的质量
        onDone: function (e) {
            //裁剪完成
            document.getElementById('previewImg').src = e;
        },
        onCancel: function(){
            //取消裁剪
        }
    });
    //实例完成后，在事件中调用以下方法即可
    clip.setSize(file[0]);    //参数是 单文件 file
</script>
```


#### 参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| dragBoxClass | <code>String</code> | block | 裁剪框类名 |
| clipRadio | <code>Number</code> | - | 裁剪比例，为0或空时裁剪无比例 格式为 4 / 3 或 width / height，width与height需是整数 |
| initialHeight | <code>Number</code> | 100 | 裁剪框初始高度 最小为30，当取值小于30时按默认值100使用(初始高度请取值在最大高度与最小高度之间) |
| initialWidth | <code>Number</code> | 100 | 裁剪框初始宽度 最小为30，当取值小于30时按默认值100使用(初始高度请取值在最大宽度与最小宽度之间) |
| minHeight | <code>Number</code> | 100 | 裁剪框最小高度 最小为30，当取值小于30时按默认值100使用 |
| minWidth | <code>Number</code> | 100 | 裁剪框最小宽度 最小为30，当取值小于30时按默认值100使用 |
| maxHeight | <code>Number</code> | 图片高度 | 裁剪框最大高度 当取值为0或不规范时按默认值图片高度使用 |
| maxWidth | <code>Number</code> | 图片宽度 | 裁剪框最大宽度 当取值为0或不规范时按默认值图片宽度使用 |
| cornerColor | <code>String</code> | #39f | 裁剪框颜色 格式为 #f00 或 red |
| encode | <code>String</code> | base64 | 导出格式，支持 base64|blob|file |
| type | <code>String</code> | png | 裁剪后图片的类型，仅支持jpeg/png两种 |
| name | <code>String</code> | img | 裁剪后的图片名，仅在导出格式为file时可用 |
| quality | <code>Number</code> | 1 | 压缩质量 |
| onDone | <code>Function</code> | - | 裁剪完成后的回调函数 回调参数1个，值为导出格式的文件数据 |
| onCancel | <code>Function</code> | - | 裁剪取消后的回调函数 |

#### 示例

```
Css
body,html{width:100%;height:100%;background:#f2f2f2;padding:0;margin:0;font-size:1em;}
.inputbox{ width: 1000px; margin: 0 auto;}
.code{background:none repeat scroll 0 0 #E3F4F9;border:1px solid #BAE2F0;font:12px "Courier New",Courier,monospace;margin:30px auto;padding:10px 10px 40px;width:980px}
.code p{height:24px;line-height:24px}
.code span{zoom:1;margin-right:5px;width:85px;font-weight:bold;color:#39f}

#clipping-container{ width: 1000px; margin: 0 auto;}
.previewImg{ display: block; width: auto; max-width: 1000px; height: auto; margin: 10px auto;}
```

```
Html
<section>
    <div class="inputbox">
        <div class="button" role="button">
			选择图片：<input type="file" name="file" class="upload-img" accept="image/*" onchange="chooseImg(this)" />
		</div>
    </div>
    <div id="clipping-container"></div>
    <img id="previewImg" src="" alt="" class="previewImg">
</section>
```

```
Javascript
function chooseImg(event){
    var files = event.files || event.dataTransfer.files,
        file = files[0] || files;
    event.value = '';
    window.clip = new Clip({
        dragBoxClass: 'block',
        clipRadio: 4 / 3,
        cornerColor: '#f00',
        maxWidth: 300,
        encode: 'base64',
        type: 'png',
        name: 'rtest',
        quality: 0.9,
        onDone: function (e) {
            document.getElementById('previewImg').src = e;
        },
        onCancel: function(){

        }
    });
    clip.setSize(file);
}
```
