# Clipping

#### 介绍
Web side image clipping component (JS, no dependencies)

#### 使用说明 CDN

```
<script src="croptool.min.js"></script>
<script>
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
            //Finish clipping
            document.getElementById('previewImg').src = e;
        },
        onCancel: function(){
            //Cancel clipping
        }
    });
    //Once the instance is complete, the following methods are called in the event
    clip.setSize(file[0]);    //file
</script>
```


#### Parameter Specification 

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| dragBoxClass | <code>String</code> | block | Crop box class |
| clipRadio | <code>Number</code> | - | The clipping ratio is 0 or the clipping format is 4/3 or width/height, width and height should be integers |
| initialHeight | <code>Number</code> | 100 | The minimum initial height of the clipping box is 30. If the value is less than 30, use the default value of 100 (the initial height should be between the maximum and minimum height). |
| initialWidth | <code>Number</code> | 100 | The minimum initial width of the clipping box is 30. If the value is less than 30, use the default value of 100 (the initial width should be between the maximum and minimum width). |
| minHeight | <code>Number</code> | 100 | The minimum height of the clipping box is 30. When the value is less than 30, the default value of 100 is used |
| minWidth | <code>Number</code> | 100 | The minimum width of the clipping box is 30, and the default value of 100 is used when the value is less than 30 |
| maxHeight | <code>Number</code> | Picture height | The maximum height of the clipping box is 0 or the default height of the picture is used when the value is not standard |
| maxWidth | <code>Number</code> | Picture width | The maximum width of the clipping box is used as the default image width when the value is 0 or not standard |
| cornerColor | <code>String</code> | #39f | The crop box color in the format #f00 or red |
| encode | <code>String</code> | base64 | Export formats, support base64 | blob | file |
| type | <code>String</code> | png | Type of cropped image, only support JPEG/PNG two kinds |
| name | <code>String</code> | img | Cropped image name, available only when exported in file format |
| quality | <code>Number</code> | 1 | The compression quality |
| onDone | <code>Function</code> | - | The callback function after clipping has 1 callback parameter, and the value is the file data in the exported format |
| onCancel | <code>Function</code> | - | Trims the callback function after cancellation |

#### Sample Code

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
			Select pictures:<input type="file" name="file" class="upload-img" accept="image/*" onchange="chooseImg(this)" />
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
