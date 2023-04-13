---
title: Spring Boot 返回CSV
date: 2021-06-20 16:00:47
tags:
categories:
---

最需要明确的一点: 不同于浏览器，axois是无法直接通过请求进行文件下载的

正确方式:

前端：

```js
axios({
        withCredentials: true,
        method: 'post',
        url: '/admin/data.csv',
        responseType: 'blob',
        timeout: 4000,
        data: this.tableData
      }).then((res) => {
        console.log(res)
        let url = window.URL.createObjectURL(new Blob([res.data]))
        let link = document.createElement('a')
        link.style.display = 'none'
        link.href = url
        link.setAttribute('download', 'data.csv')
        document.body.appendChild(link)
        link.click()
      }, ErrorEvent => {
        this.$message('请求数据失败')
      })
```

后端

```java
@RequestMapping("/admin/data.csv")
    @ResponseBody
    public void getExcel(@RequestBody JSONArray array, HttpServletResponse response) throws IOException {
        System.out.println(array);
        String csvContent = analyseService.buildCSV(array);
        response.setCharacterEncoding("utf-8");
        response.setContentType("multipart/form-data");
        response.setHeader("Content-Disposition", "attachment;fileName=data.csv");
        OutputStream out = response.getOutputStream();
        out.write(csvContent.getBytes());
    }
```

