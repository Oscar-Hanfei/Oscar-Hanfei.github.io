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
            color: #333;
            margin: 0;
            padding: 0;
            background: #fff;
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
    <!-- 音乐板块 -->
    <div id="music-toggle" style="position:fixed;top:24px;right:32px;z-index:2000;cursor:pointer;">
        <img id="download-music" src="download.png" alt="下载音乐" title="点击即可下载本歌曲" style="width:28px;height:28px;margin-right:8px;vertical-align:middle;">
        <img id="music-icon" src="music_start.png" alt="音乐开关" style="width:28px;height:28px;vertical-align:middle;">
        <audio id="music-audio" src="Parting blossoms.mp3" preload="auto" style="display:none;" controlslist="nodownload"></audio>
        <div id="lrc-panel" style="display:none;position:absolute;top:60px;right:0;width:320px;max-height:320px;overflow:auto;background:rgba(255,255,255,0.95);border-radius:8px;box-shadow:0 2px 8px #0002;padding:12px 18px 12px 18px;font-size:15px;color:#333;line-height:1.7;white-space:pre-wrap;z-index:2100;">
            <div id="lrc-text"></div>
        </div>
    </div>
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
            <li>
                 <a href="https://www.bilibili.com/video/BV1UT42167xb/?spm_id_from=..search-card.all.click&vd_source=45c9523933079a3868e63b75b451ed91" target="_blank">敬请期待</a>
                <p class="desc">《极限思想》，涵盖全领域，带你体验开挂人生</p>
                <div class="meta">⭐ 收藏 | 更新于 2025-07-01 | 提取码：暂无</div>
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
        // DOM元素获取提前，避免未定义
        const musicToggle = document.getElementById('music-toggle');
        const musicIcon = document.getElementById('music-icon');
        const musicAudio = document.getElementById('music-audio');
        const lrcPanel = document.getElementById('lrc-panel');
        const lrcText = document.getElementById('lrc-text');
        
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
        
        // LRC 歌词内容
        // 请将 Parting blossoms.lrc 的内容粘贴到下面的多行字符串中
        const lrcString = `
[00:00.06]离别开出花 - 就是南方凯
[00:01.33]曲Composer：李浩瑞
[00:02.04]词Lyricist：李浩瑞
[00:02.76]制作人Producer：刘涛/李浩瑞
[00:04.13]编曲Arranger：谭侃侃
[00:05.06]吉他&贝斯Guitar&bass：谭侃侃
[00:06.35]混音师Mixing Engineer：袁中仁
[00:07.52]母带后期混音师Mastering Engineer：袁中仁
[00:09.02]和声Backing Vocals：李浩瑞/谭侃侃/顾雄/袁中仁/夹_zZ
[00:11.38]和声编写Backing Vocals Design：李浩瑞/顾雄
[00:13.16]配唱制作人Vocal Producer：刘涛/李浩瑞
[00:14.94]录音师Recording Engineer：袁中仁
[00:16.26]人声编辑Vocal Editing：刘涛
[00:17.52]视觉设计Visual Design：kidult.
[00:18.64]监制Executive Producer：陶诗
[00:19.44]策划总监Planning Director：左三好
[00:20.66]营销推广Marketing Promoter：祝鑫
[00:20.67]混音棚：好乐无荒混音棚（长沙）
[00:20.71]录音棚Recording Studio：好乐无荒录音棚（长沙）
[00:20.74]制作公司Manufacturing Company：好乐无荒
[00:20.76]OP/SP：好乐无荒
[00:20.78]项目统筹Project Coordinator：宋旭辉Shawn Song@索尼音乐/李若嫣Ruoyan Li@索尼音乐
[00:20.83]制作统筹Production Coordinator：赵楚峰Chufeng Zhao@索尼音乐
[00:20.86]监制Deputy Executive Producer：许雯静Vivian Xu@索尼音乐/刘嘉雄Charles Liu@索尼音乐
[00:20.92]总监制Chief Executive Producer：陈国威Andrew Chan@索尼音乐
[00:20.95]联合企划Co-Present：大声密谋
[00:20.97]（本作品声明：著作权权利保留，未经许可，不得使用）
[00:21.03]坐上那朵离家的云霞
[00:25.65]飘去无人知晓的天涯
[00:30.11]背着妈妈说的那句话
[00:34.65]孩子人生其实不复杂
[00:37.80]喔～眼泪轻轻地擦
[00:41.24]别管那多嘴乌鸦
[00:43.14]咽下那些风沙
[00:45.66]你才能慢慢长大
[00:47.52]要错过几个她
[00:50.23]用你最好的年华
[00:52.35]这是青春的代价
[00:55.53]当离别开出花
[00:57.15]伸出新长的枝桠
[00:59.74]像冬去春又来
[01:01.89]等待心雪融化
[01:04.27]你每次离开家
[01:06.25]带着远方的牵挂
[01:08.82]那城市的繁华
[01:10.66]盖住了月牙
[01:13.45]当离别开出花
[01:15.76]它生长在悬崖
[01:17.85]在最高的山顶
[01:19.91]才听得见回答
[01:22.45]没什么好害怕
[01:24.28]孩子放心去飞吧
[01:27.35]在你的身后
[01:28.85]有个等你的家
[01:42.63]坐上那朵离家的云霞
[01:47.16]飘去无人知晓的天涯
[01:51.65]背着妈妈说的那句话
[01:56.18]孩子人生其实不复杂
[01:59.30]喔～眼泪轻轻地擦
[02:02.74]别忘那童年梦话
[02:04.58]散在远方的花
[02:07.21]也随风慢慢长大
[02:09.04]要错过几个她
[02:11.55]用你最真的年华
[02:13.99]这是青春的回答
[02:16.89]当离别开出花
[02:18.66]伸出新长的枝桠
[02:21.24]像冬去春又来
[02:23.11]等待心雪融化
[02:25.85]你每次离开家
[02:27.69]带着远方的牵挂
[02:30.31]那城市的繁华
[02:32.36]盖住了月牙
[02:34.86]当离别开出花
[02:37.25]它生长在悬崖
[02:39.4]在最高的山顶
[02:41.31]才听得见回答
[02:43.93]没什么好害怕
[02:45.78]孩子放心去飞吧
[02:48.73]在你的身后
[02:50.33]有个等你的家
[02:53.05]当离别开出花
[02:54.87]伸出新长的枝桠
[02:57.49]像冬去春又来
[02:59.33]等待心雪融化
[03:02.06]你每次离开家
[03:03.94]带着远方的牵挂
[03:06.53]那城市的繁华
[03:08.29]盖住了月牙
[03:11.09]当离别开出花
[03:13.45]它生长在悬崖
[03:15.63]在最高的山顶
[03:17.49]才听得见回答
[03:20.16]没什么好害怕
[03:22.0]孩子放心去飞吧
[03:24.97]在你的身后
[03:26.54001]有个等你的家
`;
        // 解析LRC
        function parseLRC(lrc) {
            const lines = lrc.split('\n');
            const result = [];
            for (let line of lines) {
                const match = line.match(/\[(\d{2}):(\d{2})\.(\d{2,3})\](.*)/);
                if (match) {
                    const min = parseInt(match[1]);
                    const sec = parseInt(match[2]);
                    const ms = parseInt(match[3].padEnd(3, '0'));
                    const time = min * 60 * 1000 + sec * 1000 + ms;
                    result.push({ time, text: match[4].trim() });
                }
            }
            return result.sort((a, b) => a.time - b.time);
        }
        const lrcData = parseLRC(lrcString);
        // 歌词同步显示
        function showLRC(currentTime) {
            let html = '';
            let found = false;
            for (let i = 0; i < lrcData.length; i++) {
                const next = lrcData[i + 1] ? lrcData[i + 1].time / 1000 : Infinity;
                if (currentTime >= lrcData[i].time / 1000 && currentTime < next) {
                    html += `<span style='color:#be6cdf;font-weight:bold;'>${lrcData[i].text}</span><br>`;
                    found = true;
                } else {
                    html += lrcData[i].text + '<br>';
                }
            }
            lrcText.innerHTML = html;
        }
        // 音乐播放时同步歌词
        musicAudio.addEventListener('timeupdate', function() {
            showLRC(musicAudio.currentTime);
        });
        // 切换音乐时显示/隐藏歌词面板
        musicToggle.onclick = function() {
            if (!isPlaying) {
                musicAudio.play().then(() => {
                    musicIcon.src = 'music_stop.png';
                    isPlaying = true;
                    lrcPanel.style.display = 'block';
                }).catch((e) => {
                    alert('浏览器限制了自动播放，请手动与页面交互后再试。');
                });
            } else {
                musicAudio.pause();
                musicAudio.currentTime = 0;
                musicIcon.src = 'music_start.png';
                isPlaying = false;
                lrcPanel.style.display = 'none';
            }
        };
        // 下载按钮功能
        const downloadBtn = document.getElementById('download-music');
        downloadBtn.addEventListener('click', function(e) {
            e.stopPropagation(); // 防止触发音乐播放
            const a = document.createElement('a');
            a.href = 'Parting blossoms.mp3';
            a.download = 'Parting blossoms.mp3';
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
        });
        downloadBtn.addEventListener('mouseenter', function() {
            downloadBtn.title = '点击即可下载本歌曲';
        });
        // 自动播放时直接切换图标和歌词面板
        window.addEventListener('DOMContentLoaded', function() {
            musicAudio.addEventListener('play', function() {
                musicIcon.src = 'music_stop.png';
                lrcPanel.style.display = 'block';
                isPlaying = true;
            });
            musicAudio.addEventListener('pause', function() {
                musicIcon.src = 'music_start.png';
                lrcPanel.style.display = 'none';
                isPlaying = false;
            });
        });
        // 音乐板块逻辑
        let isPlaying = false;
        musicToggle.onclick = function() {
            if (!isPlaying) {
                musicAudio.play().then(() => {
                    musicIcon.src = 'music_stop.png';
                    isPlaying = true;
                    lrcPanel.style.display = 'block';
                }).catch((e) => {
                    alert('浏览器限制了自动播放，请手动与页面交互后再试。');
                });
            } else {
                musicAudio.pause();
                musicAudio.currentTime = 0;
                musicIcon.src = 'music_start.png';
                isPlaying = false;
                lrcPanel.style.display = 'none';
            }
        };
        // 自动播放时直接切换图标和歌词面板
        window.addEventListener('DOMContentLoaded', function() {
            musicAudio.addEventListener('play', function() {
                musicIcon.src = 'music_stop.png';
                lrcPanel.style.display = 'block';
                isPlaying = true;
            });
            musicAudio.addEventListener('pause', function() {
                musicIcon.src = 'music_start.png';
                lrcPanel.style.display = 'none';
                isPlaying = false;
            });
        });
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
