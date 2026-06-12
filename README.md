<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Biodata 3D | Athamulia Galih | Engineer Muda</title>
    <!-- Google Fonts & Font Awesome -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <!-- Three.js CDN -->
    <script type="importmap">
        {
            "imports": {
                "three": "https://unpkg.com/three@0.128.0/build/three.module.js"
            }
        }
    </script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif;
            overflow-x: hidden;
            color: #fff;
            background-color: #0a0a2a;
        }

        /* Canvas 3D Background */
        #canvas-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            outline: none;
        }

        /* Overlay konten */
        .content {
            position: relative;
            z-index: 10;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            backdrop-filter: blur(2px);
        }

        /* Navbar / Tombol Menu */
        .menu-bar {
            display: flex;
            justify-content: center;
            gap: 1.8rem;
            padding: 1.5rem 1rem;
            background: rgba(0, 0, 0, 0.4);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
            flex-wrap: wrap;
            position: sticky;
            top: 0;
            z-index: 20;
        }

        .menu-btn {
            background: rgba(20, 30, 45, 0.75);
            border: none;
            color: white;
            font-size: 1.2rem;
            font-weight: 600;
            padding: 0.7rem 1.5rem;
            border-radius: 40px;
            cursor: pointer;
            backdrop-filter: blur(5px);
            transition: all 0.3s ease;
            font-family: 'Poppins', sans-serif;
            letter-spacing: 1px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            border: 1px solid rgba(255,255,255,0.3);
        }

        .menu-btn i {
            margin-right: 8px;
        }

        .menu-btn:hover {
            background: #ff6b4a;
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.3);
            border-color: #ffaa80;
        }

        /* Container utama biodata */
        .biodata-container {
            display: flex;
            justify-content: center;
            align-items: center;
            flex: 1;
            padding: 2rem 1.5rem 3rem;
        }

        /* Card 3D modern dengan efek glassmorphism + 3D transform */
        .card {
            background: rgba(15, 25, 45, 0.65);
            backdrop-filter: blur(12px);
            border-radius: 48px;
            padding: 2rem 2.5rem;
            max-width: 750px;
            width: 100%;
            box-shadow: 0 25px 45px rgba(0,0,0,0.3), 0 0 0 1px rgba(255,255,255,0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            border: 1px solid rgba(255,255,255,0.2);
            transform-style: preserve-3d;
            transform: perspective(1200px) rotateX(2deg) rotateY(1deg);
        }

        .card:hover {
            transform: perspective(1200px) rotateX(0deg) rotateY(0deg) translateY(-8px);
            box-shadow: 0 35px 55px rgba(0,0,0,0.4);
            background: rgba(20, 35, 60, 0.75);
        }

        /* Header profil */
        .profile-header {
            text-align: center;
            margin-bottom: 1.8rem;
            position: relative;
        }

        .avatar {
            background: linear-gradient(135deg, #ff8c5a, #ff4d6d);
            width: 110px;
            height: 110px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
            margin: 0 auto 1rem;
            box-shadow: 0 15px 35px rgba(255, 77, 109, 0.3);
            border: 3px solid rgba(255,255,240,0.7);
        }

        .avatar i {
            font-size: 4rem;
            color: white;
            text-shadow: 2px 2px 5px rgba(0,0,0,0.2);
        }

        h1 {
            font-size: 2.5rem;
            font-weight: 800;
            background: linear-gradient(120deg, #fff, #ffbc8c);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            letter-spacing: 1px;
        }

        .tagline {
            font-size: 1rem;
            opacity: 0.9;
            margin-top: 0.3rem;
            letter-spacing: 1px;
        }

        /* Grid info */
        .info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 1.2rem;
            margin: 2rem 0;
        }

        .info-item {
            background: rgba(0,0,0,0.35);
            border-radius: 24px;
            padding: 1rem 1.2rem;
            transition: all 0.2s;
            border-left: 4px solid #ff6b4a;
        }

        .info-label {
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            font-weight: 500;
            color: #ffc8a2;
        }

        .info-value {
            font-size: 1.3rem;
            font-weight: 700;
            margin-top: 6px;
            word-break: break-word;
        }

        .desc-section {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 28px;
            padding: 1.2rem 1.5rem;
            margin: 1.5rem 0;
            text-align: center;
        }

        .desc-section h3 {
            font-size: 1.5rem;
            margin-bottom: 0.7rem;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .desc-section p {
            line-height: 1.6;
            font-size: 1rem;
            font-weight: 400;
        }

        /* Tombol Project Game */
        .game-btn-wrapper {
            text-align: center;
            margin-top: 1.5rem;
            margin-bottom: 0.5rem;
        }

        .btn-project {
            background: linear-gradient(95deg, #ff4d6d, #ff9e4a);
            border: none;
            padding: 1rem 2rem;
            font-size: 1.2rem;
            font-weight: bold;
            border-radius: 60px;
            color: white;
            cursor: pointer;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 12px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.3);
            border: 1px solid rgba(255,255,200,0.5);
            font-family: 'Poppins', sans-serif;
            text-decoration: none;
        }

        .btn-project i {
            font-size: 1.4rem;
        }

        .btn-project:hover {
            transform: scale(1.05);
            background: linear-gradient(95deg, #ff6d8a, #ffb46a);
            box-shadow: 0 18px 30px rgba(0,0,0,0.4);
        }

        /* Footer */
        footer {
            text-align: center;
            padding: 1.5rem;
            font-size: 0.8rem;
            background: rgba(0,0,0,0.5);
            backdrop-filter: blur(5px);
            margin-top: auto;
        }

        /* Responsif */
        @media (max-width: 600px) {
            .card {
                padding: 1.5rem;
            }
            h1 {
                font-size: 1.8rem;
            }
            .info-value {
                font-size: 1rem;
            }
            .menu-btn {
                padding: 0.4rem 1rem;
                font-size: 0.9rem;
            }
            .avatar {
                width: 80px;
                height: 80px;
            }
            .avatar i {
                font-size: 2.8rem;
            }
        }

        /* animasi fade untuk konten */
        .fade-section {
            transition: all 0.3s ease;
        }
    </style>
</head>
<body>

<div id="canvas-container"></div>

<div class="content">
    <div class="menu-bar">
        <button class="menu-btn" id="btn-home"><i class="fas fa-user-astronaut"></i> Beranda</button>
        <button class="menu-btn" id="btn-bio"><i class="fas fa-id-card"></i> Biodata</button>
        <button class="menu-btn" id="btn-desc"><i class="fas fa-align-left"></i> Deskripsi</button>
        <button class="menu-btn" id="btn-game"><i class="fas fa-gamepad"></i> Project Game</button>
    </div>

    <div class="biodata-container" id="mainContent">
        <div class="card" id="dynamicCard">
            <div id="cardInner">
                <!-- Konten akan diisi dinamis oleh JS -->
            </div>
        </div>
    </div>
    <footer>
        <i class="fas fa-cube"></i> 3D Interactive Biodata | Athamulia Galih © 2026 | Engineer Future
    </footer>
</div>

<script type="module">
    import * as THREE from 'three';

    // --- Setup 3D Scene ---
    const container = document.getElementById('canvas-container');
    const scene = new THREE.Scene();
    scene.background = new THREE.Color(0x050b1a);
    scene.fog = new THREE.FogExp2(0x050b1a, 0.008);

    const camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.set(0, 2, 8);
    camera.lookAt(0, 0, 0);

    const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: false });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.shadowMap.enabled = true;
    renderer.setPixelRatio(window.devicePixelRatio);
    container.appendChild(renderer.domElement);

    // --- Lighting ---
    const ambientLight = new THREE.AmbientLight(0x404060);
    scene.add(ambientLight);
    const dirLight = new THREE.DirectionalLight(0xfff5e0, 1.2);
    dirLight.position.set(3, 5, 2);
    dirLight.castShadow = true;
    dirLight.receiveShadow = true;
    scene.add(dirLight);
    const backLight = new THREE.PointLight(0x4466cc, 0.5);
    backLight.position.set(-2, 1, -3);
    scene.add(backLight);
    const rimLight = new THREE.PointLight(0xffaa66, 0.6);
    rimLight.position.set(1, 2, 2);
    scene.add(rimLight);
    const fillLight = new THREE.PointLight(0x77aaff, 0.4);
    fillLight.position.set(-1, 1, 2);
    scene.add(fillLight);
    
    // tambahan lampu senter dari bawah
    const fillBottom = new THREE.PointLight(0xff8866, 0.3);
    fillBottom.position.set(0, -2, 1);
    scene.add(fillBottom);

    // --- Core 3D Objects: Futuristic Rotating Core + Rings + Particles ---
    const mainGroup = new THREE.Group();
    scene.add(mainGroup);
    
    // Torus Knot utama
    const geometryKnot = new THREE.TorusKnotGeometry(0.9, 0.22, 180, 24, 3, 4);
    const materialKnot = new THREE.MeshStandardMaterial({ color: 0xff6b4a, emissive: 0x442211, roughness: 0.3, metalness: 0.7 });
    const knot = new THREE.Mesh(geometryKnot, materialKnot);
    knot.castShadow = true;
    mainGroup.add(knot);
    
    // Icosahedron dalam
    const icoGeo = new THREE.IcosahedronGeometry(0.45, 0);
    const icoMat = new THREE.MeshStandardMaterial({ color: 0xffaa77, emissive: 0x331100, metalness: 0.6, roughness: 0.2 });
    const coreIco = new THREE.Mesh(icoGeo, icoMat);
    coreIco.castShadow = true;
    mainGroup.add(coreIco);
    
    // Ring horizontal
    const ringGeo = new THREE.TorusGeometry(1.1, 0.05, 64, 200);
    const ringMat = new THREE.MeshStandardMaterial({ color: 0xff8c5a, emissive: 0xff3300, metalness: 0.9 });
    const ring = new THREE.Mesh(ringGeo, ringMat);
    ring.rotation.x = Math.PI / 2;
    mainGroup.add(ring);
    
    // Ring miring kedua
    const ring2Geo = new THREE.TorusGeometry(1.25, 0.04, 64, 200);
    const ring2Mat = new THREE.MeshStandardMaterial({ color: 0xffaa88, emissive: 0x662200 });
    const ring2 = new THREE.Mesh(ring2Geo, ring2Mat);
    ring2.rotation.z = Math.PI / 3;
    ring2.rotation.x = Math.PI / 4;
    mainGroup.add(ring2);
    
    // Particle sphere
    const particleCount = 1000;
    const particlesGeometry = new THREE.BufferGeometry();
    const positions = new Float32Array(particleCount * 3);
    for (let i = 0; i < particleCount; i++) {
        const radius = 1.6 + Math.random() * 0.6;
        const theta = Math.random() * Math.PI * 2;
        const phi = Math.acos(2 * Math.random() - 1);
        positions[i*3] = radius * Math.sin(phi) * Math.cos(theta);
        positions[i*3+1] = radius * Math.sin(phi) * Math.sin(theta) * 0.8;
        positions[i*3+2] = radius * Math.cos(phi);
    }
    particlesGeometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
    const particleMat = new THREE.PointsMaterial({ color: 0xffaa88, size: 0.035, transparent: true, blending: THREE.AdditiveBlending });
    const particleSystem = new THREE.Points(particlesGeometry, particleMat);
    mainGroup.add(particleSystem);
    
    // Floating stars background
    const starCount = 1500;
    const starGeo = new THREE.BufferGeometry();
    const starPos = new Float32Array(starCount * 3);
    for (let i = 0; i < starCount; i++) {
        starPos[i*3] = (Math.random() - 0.5) * 200;
        starPos[i*3+1] = (Math.random() - 0.5) * 100;
        starPos[i*3+2] = (Math.random() - 0.5) * 80 - 40;
    }
    starGeo.setAttribute('position', new THREE.BufferAttribute(starPos, 3));
    const starMat = new THREE.PointsMaterial({ color: 0xffffff, size: 0.08, transparent: true, opacity: 0.6 });
    const stars = new THREE.Points(starGeo, starMat);
    scene.add(stars);
    
    // Kubus kecil berputar disekitar
    const cubeGroup = new THREE.Group();
    const cubeMatSmall = new THREE.MeshStandardMaterial({ color: 0xffaa66, emissive: 0x442200 });
    for (let i = 0; i < 70; i++) {
        const size = 0.05 + Math.random() * 0.08;
        const cube = new THREE.Mesh(new THREE.BoxGeometry(size, size, size), cubeMatSmall);
        const rad = 1.4 + Math.random() * 1.0;
        const angle = Math.random() * Math.PI * 2;
        const height = (Math.random() - 0.5) * 1.8;
        cube.position.x = Math.cos(angle) * rad;
        cube.position.z = Math.sin(angle) * rad;
        cube.position.y = height;
        cube.castShadow = true;
        cubeGroup.add(cube);
    }
    mainGroup.add(cubeGroup);
    
    // Animasi mouse
    let mouseX = 0, mouseY = 0;
    document.addEventListener('mousemove', (event) => {
        mouseX = (event.clientX / window.innerWidth) * 2 - 1;
        mouseY = (event.clientY / window.innerHeight) * 2 - 1;
    });
    
    let time = 0;
    function animate3D() {
        requestAnimationFrame(animate3D);
        time += 0.009;
        
        mainGroup.rotation.y = time * 0.5;
        mainGroup.rotation.x = Math.sin(time * 0.3) * 0.1;
        mainGroup.rotation.z = Math.cos(time * 0.5) * 0.05;
        
        knot.rotation.x = time * 0.6;
        knot.rotation.z = time * 0.4;
        coreIco.rotation.y = time * 0.8;
        ring.rotation.z = time * 0.3;
        ring2.rotation.y = time * 0.5;
        ring2.rotation.x = Math.PI / 4 + Math.sin(time) * 0.1;
        
        cubeGroup.children.forEach((child) => {
            child.rotation.x += 0.02;
            child.rotation.y += 0.03;
        });
        
        const targetX = mouseX * 0.5;
        const targetY = mouseY * 0.3;
        camera.position.x += (targetX - camera.position.x) * 0.05;
        camera.position.y += (targetY - camera.position.y) * 0.05;
        camera.lookAt(0, 0.5, 0);
        
        stars.rotation.y += 0.0005;
        stars.rotation.x += 0.0003;
        
        renderer.render(scene, camera);
    }
    animate3D();
    
    window.addEventListener('resize', onWindowResize, false);
    function onWindowResize() {
        camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
    }
    
    // --- KONTEN DINAMIS BERDASARKAN DATA TERBARU ---
    // Data: Nama lengkap Athamulia Galih, TTL Bekasi 19 Agustus 2009, Hobi futsal, cita-cita Engineer, Kelas 11, sekolah SMA Al-Muslim
    
    const contents = {
        home: `
            <div class="profile-header">
                <div class="avatar">
                    <i class="fas fa-futbol"></i>
                </div>
                <h1>Athamulia Galih</h1>
                <div class="tagline"><i class="fas fa-map-marker-alt"></i> Bekasi, 19 Agustus 2009 | Engineer Muda</div>
            </div>
            <div class="info-grid">
                <div class="info-item"><div class="info-label"><i class="fas fa-calendar-alt"></i> TTL</div><div class="info-value">Bekasi, 19 Agustus 2009</div></div>
                <div class="info-item"><div class="info-label"><i class="fas fa-futbol"></i> Hobi Utama</div><div class="info-value">Futsal ⚽</div></div>
                <div class="info-item"><div class="info-label"><i class="fas fa-microchip"></i> Cita-cita</div><div class="info-value">Engineer</div></div>
                <div class="info-item"><div class="info-label"><i class="fas fa-school"></i> Sekolah & Kelas</div><div class="info-value">SMA Al-Muslim | Kelas 11</div></div>
            </div>
            <div class="desc-section">
                <h3><i class="fas fa-quote-left"></i> Semangat Engineer Muda</h3>
                <p>Halo! Saya Athamulia Galih, lahir di Bekasi, 19 Agustus 2009. Saat ini duduk di kelas 11 SMA Al-Muslim. Hobi futsal membuat saya disiplin dan bugar, sementara cita-cita saya adalah menjadi Engineer handal yang berkontribusi untuk teknologi masa depan.</p>
            </div>
            <div class="game-btn-wrapper">
                <a href="https://athamulia-cpu.github.io/Tembak-Bimo-Ganteng/" target="_blank" rel="noopener noreferrer" class="btn-project">
                    <i class="fas fa-gamepad"></i> Main Game: Tembak Bimo Ganteng
                </a>
            </div>
        `,
        biodata: `
            <div class="profile-header">
                <div class="avatar" style="background: linear-gradient(135deg, #2a6f8f, #4c3b8c);">
                    <i class="fas fa-id-card"></i>
                </div>
                <h1>Biodata Diri</h1>
                <div class="tagline"><i class="fas fa-user-graduate"></i> Detail Lengkap</div>
            </div>
            <div class="info-grid">
                <div class="info-item"><div class="info-label">Nama Lengkap</div><div class="info-value">Athamulia Galih</div></div>
                <div class="info-item"><div class="info-label">Tempat, Tanggal Lahir</div><div class="info-value">Bekasi, 19 Agustus 2009</div></div>
                <div class="info-item"><div class="info-label">Usia (2026)</div><div class="info-value">16 Tahun</div></div>
                <div class="info-item"><div class="info-label">Hobi</div><div class="info-value">Futsal (Penyuka Sepak Bola)</div></div>
                <div class="info-item"><div class="info-label">Cita-cita</div><div class="info-value">Engineer (Teknik & Teknologi)</div></div>
                <div class="info-item"><div class="info-label">Pendidikan</div><div class="info-value">SMA Al-Muslim, Kelas 11</div></div>
            </div>
            <div class="desc-section">
                <h3><i class="fas fa-tools"></i> Profil Singkat</h3>
                <p>Athamulia Galih, lahir di Bekasi 19 Agustus 2009. Sejak kecil gemar merangkai dan memahami cara kerja mesin. Saat ini menempuh pendidikan di SMA Al-Muslim kelas 11, aktif dalam kegiatan futsal dan ekskul robotika. Target: menjadi engineer profesional.</p>
            </div>
            <div class="game-btn-wrapper">
                <a href="https://athamulia-cpu.github.io/Tembak-Bimo-Ganteng/" target="_blank" class="btn-project">
                    <i class="fas fa-gamepad"></i> Project Game
                </a>
            </div>
        `,
        deskripsi: `
            <div class="profile-header">
                <div class="avatar" style="background: linear-gradient(135deg, #3b9e7c, #2b6d8f);">
                    <i class="fas fa-pen-fancy"></i>
                </div>
                <h1>Deskripsi & Mimpi</h1>
                <div class="tagline">Perjalanan Menuju Engineer</div>
            </div>
            <div class="desc-section" style="background: rgba(0,0,0,0.4); margin-top:0.5rem;">
                <h3><i class="fas fa-cogs"></i> "Engineer adalah jalan hidupku"</h3>
                <p>Saya Athamulia Galih, lahir di Bekasi 19 Agustus 2009. Saat ini kelas 11 di SMA Al-Muslim. Futsal adalah hobi yang mengajarkan teamwork, kecepatan berpikir, dan strategi. Namun panggilan jiwa saya adalah di bidang engineering — menciptakan solusi, merancang sistem, dan membangun masa depan dengan teknologi. Saya percaya bahwa kombinasi olahraga dan sains membentuk pribadi yang tangguh.</p>
                <hr style="margin: 1rem 0; border-color:rgba(255,255,255,0.2)">
                <p><i class="fas fa-futbol"></i> Futsal mengajarkan saya untuk pantang menyerah, sementara dunia teknik memicu rasa ingin tahu saya. Cita-cita: menjadi Engineer yang membanggakan keluarga dan bangsa.</p>
                <p style="margin-top: 12px;"><i class="fas fa-rocket"></i> "Bangun negeri melalui karya engineer muda"</p>
            </div>
            <div class="game-btn-wrapper">
                <a href="https://athamulia-cpu.github.io/Tembak-Bimo-Ganteng/" target="_blank" class="btn-project">
                    <i class="fas fa-rocket"></i> Coba Game Saya
                </a>
            </div>
        `,
        projectgame: `
            <div class="profile-header">
                <div class="avatar" style="background: linear-gradient(135deg, #e85d04, #ffb703);">
                    <i class="fas fa-gamepad"></i>
                </div>
                <h1>Project Game</h1>
                <div class="tagline">"Tembak Bimo Ganteng" - Action Game by Athamulia</div>
            </div>
            <div class="desc-section">
                <h3><i class="fas fa-code-branch"></i> Karya Athamulia Galih</h3>
                <p>Game tembak-tembakan seru berbasis web, dibuat dengan HTML5, CSS, dan JavaScript. Tantang refleksmu dan raih skor tertinggi! Proyek ini adalah wujud eksplorasi saya di bidang front-end dan game development. Klik tombol di bawah untuk bermain langsung.</p>
                <div style="margin: 1.5rem 0; background: rgba(0,0,0,0.5); padding: 0.8rem; border-radius: 20px;">
                    <i class="fas fa-link"></i> <strong>Link resmi:</strong> 
                    <span style="word-break:break-all; font-family:monospace;">athamulia-cpu.github.io/Tembak-Bimo-Ganteng/</span>
                </div>
                <p><i class="fas fa-star"></i> Terus belajar dan berkreasi untuk menjadi Engineer handal!</p>
            </div>
            <div class="game-btn-wrapper">
                <a href="https://athamulia-cpu.github.io/Tembak-Bimo-Ganteng/" target="_blank" class="btn-project" style="background: #ff5e00; padding: 1rem 2.2rem;">
                    <i class="fas fa-bullseye"></i> MAIN SEKARANG
                </a>
            </div>
        `
    };
    
    const cardInner = document.getElementById('cardInner');
    function setActiveContent(menuId) {
        if (menuId === 'btn-home') cardInner.innerHTML = contents.home;
        else if (menuId === 'btn-bio') cardInner.innerHTML = contents.biodata;
        else if (menuId === 'btn-desc') cardInner.innerHTML = contents.deskripsi;
        else if (menuId === 'btn-game') cardInner.innerHTML = contents.projectgame;
        
        const cardDiv = document.getElementById('dynamicCard');
        cardDiv.style.transform = 'scale(0.98)';
        setTimeout(() => {
            cardDiv.style.transform = '';
        }, 150);
    }
    
    document.getElementById('btn-home').addEventListener('click', () => setActiveContent('btn-home'));
    document.getElementById('btn-bio').addEventListener('click', () => setActiveContent('btn-bio'));
    document.getElementById('btn-desc').addEventListener('click', () => setActiveContent('btn-desc'));
    document.getElementById('btn-game').addEventListener('click', () => setActiveContent('btn-game'));
    
    // Inisialisasi awal dengan halaman home (data terbaru)
    cardInner.innerHTML = contents.home;
    console.log('3D Biodata Athamulia Galih - Bekasi, 19 Agustus 2009 - Engineer Muda');
</script>
</body>
</html>
