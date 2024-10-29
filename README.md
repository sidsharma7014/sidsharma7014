<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Photo Gallery</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f0f0f0;
        }
        h1 {
            text-align: center;
        }
        .upload-section {
            text-align: center;
            margin-bottom: 20px;
        }
        .upload-section input[type="file"] {
            display: none;
        }
        .upload-section label {
            padding: 10px 15px;
            background-color: #007bff;
            color: white;
            border-radius: 5px;
            cursor: pointer;
        }
        .gallery {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
        }
        .gallery img {
            margin: 10px;
            border: 2px solid #ddd;
            border-radius: 4px;
            width: 200px; /* Adjust as needed */
            height: auto;
            transition: transform 0.2s;
            cursor: pointer;
        }
        .gallery img:hover {
            transform: scale(1.05);
        }
        .lightbox {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            justify-content: center;
            align-items: center;
        }
        .lightbox img {
            max-width: 90%;
            max-height: 90%;
        }
        .lightbox .close {
            position: absolute;
            top: 20px;
            right: 30px;
            color: white;
            font-size: 30px;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <h1>Photo Gallery</h1>
    <div class="upload-section">
        <label for="upload">Upload Photos</label>
        <input type="file" id="upload" accept="image/*" multiple onchange="displayImages(this)">
    </div>

    <div class="gallery" id="gallery"></div>

    <div class="lightbox" id="lightbox" onclick="closeLightbox()">
        <span class="close">&times;</span>
        <img id="lightboxImage">
    </div>

    <script>
        function displayImages(input) {
            const gallery = document.getElementById('gallery');
            gallery.innerHTML = ''; // Clear existing images

            const files = input.files;
            for (let i = 0; i < files.length; i++) {
                const reader = new FileReader();
                reader.onload = function (e) {
                    const img = document.createElement('img');
                    img.src = e.target.result;
                    img.onclick = function() { openLightbox(e.target.result); };
                    gallery.appendChild(img);
                }
                reader.readAsDataURL(files[i]);
            }
        }

        function openLightbox(imageSrc) {
            const lightbox = document.getElementById('lightbox');
            const lightboxImage = document.getElementById('lightboxImage');
            lightboxImage.src = imageSrc;
            lightbox.style.display = 'flex';
        }

        function closeLightbox() {
            const lightbox = document.getElementById('lightbox');
            lightbox.style.display = 'none';
        }
    </script>

</body>
</html>
