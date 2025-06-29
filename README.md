<!DOCTYPE html>
<html lang="zh-cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>欢迎 welcome</title>
    <!-- Favicon设置 -->
    <link rel="icon" href="favicon-32x32.ico" type="image/x-icon">
    <link rel="shortcut icon" href="favicon-32x32.ico" type="image/x-icon">
    <link rel="icon" type="image/png" href="favicon-32x32.png" sizes="32x32">
    <link rel="icon" type="image/png" href="favicon-16x16.png" sizes="16x16">
    <link rel="apple-touch-icon" href="apple-touch-icon.png">
    
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            color: #33333300;
            margin: 0;
            padding: 0;
            background: url('背景.png') no-repeat center center fixed;
            background-size: cover;
            min-height: 100vh;
            position: relative;
        }
        
        /* 添加一个透明的背景层 */
        body::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(255, 255, 255, 0);
            z-index: -1;
        }
        
        /* 容器样式 */
        .container {
            max-width: 800px;
            margin: 60px auto;
            background: rgba(255, 255, 255, 0);
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 5px 25px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(0.1px); /*设置body部分模糊程度*/
        }
        
        h1 {
            text-align: center;
            margin-bottom: 40px;
            color: #2c3e50;
            font-weight: 600;
            position: relative;
            padding-bottom: 15px;
        }
        
        h1::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 3px;
            background: linear-gradient(to right, #5db9f7, #be6cdf);
        }
        
        ul {
            list-style: none;
            padding: 0;
        }
        
        li {
            margin-bottom: 30px;
            padding: 20px;
            border-radius: 8px;
            transition: all 0.3s ease;
            background: rgba(255, 255, 255, 0.18);  /*设置li部分背景透明度*/
            border-left: 4px solid #3498db;
            overflow: hidden;
            max-height: 100px;
            position: relative;
        }
        
        li:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.322);  
            background: rgba(255, 255, 255, 0.9);
            max-height: 800px;
        }
        
        a {
            color: #0e4c75;
            text-decoration: none;
            font-size: 1.2em;
            font-weight: 500;
            display: inline-block;
            margin-bottom: 5px;
        }
        
        a:hover {
            color: #cd918b;
            text-decoration: none;
        }
        
        .desc {
            color: #555;
            margin: 8px 0;
            font-size: 1em;
            line-height: 1.5;
        }
        
        .meta {
            color: #7f8c8d;
            font-size: 0.92em;
            display: flex;
            align-items: center;
        }
        
        .meta::before {
            content: '•';
            margin: 0 8px;
            color: #bdc3c7;
        }
        
        /* 多图预览容器 */
        .preview-container {
            margin-top: 15px;
            opacity: 0;
            transition: opacity 0.3s ease;
            max-height: 0;
            overflow: hidden;
        }
        
        li:hover .preview-container {
            opacity: 1;
            max-height: 700px;
        }
        
        /* 图片网格布局 */
        .image-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            gap: 10px;
            margin-top: 10px;
        }
        
        /* 预览图片样式 */
        .preview-img {
            width: 100%;
            height: 120px;
            object-fit: cover;
            border-radius: 5px;
            cursor: pointer;
            transition: transform 0.3s ease;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.2);
        }
        
        .preview-img:hover {
            transform: scale(1.05);
        }
        
        /* 放大图片的模态框 */
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.9);
            overflow: auto;
            animation: fadeIn 0.3s;
        }
        
        .modal-content {
            margin: auto;
            display: block;
            max-width: 90%;
            max-height: 90%;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            border-radius: 5px;
        }
        
        .close {
            position: absolute;
            top: 20px;
            right: 30px;
            color: #fff;
            font-size: 35px;
            font-weight: bold;
            cursor: pointer;
            transition: color 0.3s;
        }
        
        .close:hover {
            color: #ccc;
        }
        
        /* 导航箭头 */
        .prev, .next {
            position: absolute;
            top: 50%;
            width: auto;
            padding: 16px;
            margin-top: -22px;
            color: white;
            font-weight: bold;
            font-size: 20px;
            cursor: pointer;
            transition: 0.3s;
            user-select: none;
        }
        
        .next {
            right: 0;
            border-radius: 3px 0 0 3px;
        }
        
        .prev {
            left: 0;
            border-radius: 0 3px 3px 0;
        }
        
        .prev:hover, .next:hover {
            background-color: rgba(0, 0, 0, 0.8);
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            .container {
                margin: 30px 20px;
                padding: 25px;
            }
            
            h1 {
                font-size: 1.8em;
                margin-bottom: 30px;
            }
            
            li {
                max-height: 120px;
            }
            
            li:hover {
                max-height: 900px;
            }
            
            .image-grid {
                grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            }
            
            .preview-img {
                height: 100px;
            }
        }
        
        @keyframes fadeIn {
            from {opacity: 0;}
            to {opacity: 1;}
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Hanfei---的项目作品集</h1>
        <ul>
            <li>
                <a href="https://www.123865.com/s/KiwrTd-rQ40v" target="_blank">烟花模拟器</a>
                <p class="desc">一个精美的烟花模拟器，可以自定义烟花效果和颜色，带来视觉盛宴。</p> 
                <div class="meta">⭐ 收藏 | 更新于 2025-06-20 | 提取码：0620</div>
                <div class="preview-container">
                    <div class="image-grid">
                        <img src="yh1.png" class="preview-img" alt="烟花模拟器预览1" onclick="openModal(this, 'fireworks')">  
                    </div>
                </div>
            </li>
            <li>
                <a href="https://www.123865.com/s/KiwrTd-bm40v" target="_blank">图片查看器</a>
                <p class="desc">一个打包好了的exe程序，虽然不知道有啥用</p>
                <div class="meta">⭐ 收藏 | 更新于 2025-06-29 | 提取码：9261</div>
                <div class="preview-container">
                    <div class="image-grid">
                        <img src="tp1.png" class="preview-img" alt="五子棋网页版预览1" onclick="openModal(this, 'gobang')">
                        <img src="tp2.png" class="preview-img" alt="五子棋网页版预览2" onclick="openModal(this, 'gobang')">
                </div>
            </li>
            <li>
                <a href="https://www.123865.com/s/KiwrTd-KQ40v提取码:2202" target="_blank">游戏商店网站模板</a>
                <p class="desc">响应式游戏商店网站模板，适合各类游戏展示和销售，包含完整的前端界面。</p>
                <div class="meta">⭐ 收藏 | 更新于 2025-06-20 | 提取码：2202</div>
                <div class="preview-container">
                    <div class="image-grid">
                        <img src="ld1.png" class="preview-img" alt="游戏商店模板预览1" onclick="openModal(this, 'gamestore')">
                        <img src="ld2.png" class="preview-img" alt="游戏商店模板预览2" onclick="openModal(this, 'gamestore')">
                    </div>
                </div>
            </li>
            <!-- 你可以继续手动添加更多项目 -->
        </ul>
    </div>

    <!-- 图片放大查看的模态框 -->
    <div id="imageModal" class="modal">
        <span class="close" onclick="closeModal()">&times;</span>
        <a class="prev" onclick="plusSlides(-1)">&#10094;</a>
        <a class="next" onclick="plusSlides(1)">&#10095;</a>
        <img class="modal-content" id="modalImage">
    </div>

    <script>
        // 当前显示的图片索引
        let currentSlideIndex = 0; 
        // 当前项目的图片组
        let currentImageGroup = [];
        
        // 打开模态框并显示点击的图片
        function openModal(img, groupName) {
            const modal = document.getElementById('imageModal');
            const modalImg = document.getElementById('modalImage');
            
            // 获取当前项目的所有图片
            currentImageGroup = Array.from(document.querySelectorAll(`[onclick*="${groupName}"]`));
            currentSlideIndex = currentImageGroup.indexOf(img);
            
            modal.style.display = "block";
            modalImg.src = img.src;
            modalImg.alt = img.alt;
            
            // 点击模态框背景关闭
            modal.onclick = function(event) {
                if (event.target === modal) {
                    closeModal();
                }
            }
            
            // 按ESC键关闭
            document.addEventListener('keydown', function(event) {
                if (event.key === 'Escape') {
                    closeModal();
                }
            });
        }
        
        // 关闭模态框
        function closeModal() {
            document.getElementById('imageModal').style.display = "none";
        }
        
        // 切换图片
        function plusSlides(n) {
            currentSlideIndex += n;
            
            // 循环处理
            if (currentSlideIndex >= currentImageGroup.length) {
                currentSlideIndex = 0;
            } else if (currentSlideIndex < 0) {
                currentSlideIndex = currentImageGroup.length - 1;
            }
            
            document.getElementById('modalImage').src = currentImageGroup[currentSlideIndex].src;
            document.getElementById('modalImage').alt = currentImageGroup[currentSlideIndex].alt;
        }
    </script>
    <!-- 新增的页脚 -->
    <footer class="site-footer">
        <div class="footer-content">
            <div class="footer-info">
                <p>Oscar 版权所有</p>
                <p>个人资源分享网站</p>
                <p>联系方式: 209524484（QQ）</p>
            </div>
        </div>
    </footer>

    <style>
        /* 新增的页脚样式 */
        .site-footer {
            background-color: #f5f5f5cc;
            padding: 10px 0;  /*设置上下内边距*/
            font-size: 7px;  /*设置字体大小*/
            color: #151111;
            border-top: 1px solid #e5e5e57d;
            margin-top: 40px;  /*设置上外边距*/
        }
        
        .footer-content {
            max-width: 800px;  /*设置最大宽度*/
            margin: 0 auto;
            padding: 0 20px;
            text-align: center;
        }
        
        .footer-links {
            margin-bottom: 15px;
        }
        
        .footer-links a {
            color: #555;
            margin: 0 15px;
            text-decoration: none;
        }
        
        .footer-links a:hover {
            color: #333;
            text-decoration: underline;
        }
        
        .footer-info p {
            margin: 5px 0;
            line-height: 1.5;
        }
        
        @media (max-width: 768px) {
            .footer-links a {
                display: block;
                margin: 10px 0;
            }
        }
    </style>
</body>
</body>

</html>
