<script>    
    const banners = ['https://d1jyxxz9imt9yb.cloudfront.net/animal/291/meta_image/regular/leopard_7.jpg', 
    'https://i.natgeofe.com/k/3550b018-dc62-4650-829f-ee0e2a95fc6d/amur-leopard-snow.jpg?wp=1&w=1084.125&h=813.75',
    'https://upload.wikimedia.org/wikipedia/commons/4/45/Panthera_pardus_orientalis_Colchester_Zoo_%281%29.jpg',
    'https://biaza.org.uk/userfiles/news/Amur%20leopard%20YWP.PNG?w=900&hash=b2d9afa9eeb68a06b2b6b510b24e8fd7',
    'https://files.worldwildlife.org/wwfcmsprod/images/Amur_Leopard/story_full_width/7ywlql1jre_amur_leopard_65513125.jpg',
    'https://zoo-granby.transforms.svdcdn.com/production/animals/Zoo-de-Granby_Header_1920x1280_Leopard-de-lAmour.jpg?w=3405&h=2269&q=90&auto=format%2Cavif&fit=crop&crop=focalpoint&fp-x=0.2514&fp-y=0.5096&dm=1715458236&s=9e928e78561fb1c8ef06442492012a24',
    'https://images.takeshape.io/86ce9525-f5f2-4e97-81ba-54e8ce933da7/dev/b3f2f3e4-7029-4474-a542-5cbdba406cde/dreamstime_m_2378338.jpg?auto=compress%2Cformat&w=1440',
    'https://scontent-hou1-1.xx.fbcdn.net/v/t39.30808-6/486792106_1099622315528742_6897437893895544486_n.jpg?_nc_cat=104&ccb=1-7&_nc_sid=127cfc&_nc_ohc=1MhTVTbqqBkQ7kNvwEWgUna&_nc_oc=Adn9c2AJbvbhmd5DwjNE8IFzQsZFwFnM_d4Ch9B3e7ePWiGon8s6-Fzkr_OvAcssrQE&_nc_zt=23&_nc_ht=scontent-hou1-1.xx&_nc_gid=bDEJTAYvAS6al1vGlhWW7g&oh=00_AfX0cL2ehGkQl53DItToG3qcQ3DLQgNwFaPwVxOBXD2Edg&oe=68A69B28',
    ]
    let idx = $state(0);
    setInterval(() => {
        idx++;
        if (idx >= banners.length) idx = 0;
    }, 10000);
</script>

<style>
    #banner {
        position: relative;
        overflow: hidden;
        min-height: 50vw;
        height: 50vw;
        max-height: 50vw;
    }
</style>

<div style="background:url({banners[idx]}) center / cover no-repeat" id="banner" class="mask-grad-down grid-stack place-content-center w-full">
    <div class="col-start-1 row-start-1 place-content-center text-slate-50 mix-blend-luminosity">
        <h1 id="title" class="text-center">Amur Leopard</h1>
    </div>
</div>