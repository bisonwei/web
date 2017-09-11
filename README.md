hello everybody <br>

base64编码解码js：http://www.cnblogs.com/pengchengzhong/p/6027663.html
文件读取：(function () {
    paic.registerNamespace("paic.util");
    paic.util.dataURIScheme = function (id, callback, readAsText) {
        var fileEl = document.getElementById(id);
        if (fileEl && fileEl.files && fileEl.files.length == 1) {
            var file = fileEl.files[0];
            var reader = new FileReader();
            reader.onload = function () {
                callback(this.result, file);
            }
            if(readAsText) {
                reader.readAsText(file, "utf-8");
            } else {
                reader.readAsDataURL(file);
            }
        } else if(fileEl && fileEl.files && fileEl.files.length > 1) {
            var fileList = fileEl.files;
            var files = [];
            var j = 0;
            for( var i = 0 ; i < fileList.length ; i++ ){
                var reader = new FileReader();
                reader.onload = function () {
                    files.push({
                        name: fileList[j].name,
                        base64: this.result.split(",")[1]
                    });
                    if(j == fileList.length - 1) {
                        callback(files, fileList);
                    }
                    j++;
                }
                reader.readAsDataURL(fileList[i]);
            }
        }
    }
}());
