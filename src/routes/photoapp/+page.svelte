
<script>
    let image = "https://picsum.photos/id/70/367/267"
    let photo = "https://picsum.photos/id/88/367/267"
    let picture = "https://picsum.photos/id/93/367/267"
    </script>


    <div class="photos">
        <div class="image-wrapper">
            <img src={image} alt="flexbox rules">
        </div>
        <div class="image-wrapper">
            <img src={photo} alt="flexbox rules">
        </div>
        <div class="image-wrapper">
            <img src={picture} alt="flexbox vs gridbox">
        </div>
    </div>



    <style>
        /* Enkel CSS-stil för att hantera bildlayout */
        .photos {
            display: flex;
            flex-wrap: wrap;
            width: 90vw;
            gap: 50px;
            padding: 150px;
        }
        .image-wrapper {
            flex: 1 /* 3 kolumner för bredbildsskärmar */
        }
        .image-wrapper img {
            width: 100%;
            height: auto;
        }
    </style>