<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bio-Fix | Sistema Profesional</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700;900&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; background-color: #f8fafc; color: #1e293b; }
        .glass { background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(10px); }
        .card-shadow { box-shadow: 0 4px 25px -5px rgba(0,0,0,0.05); }
        .hidden { display: none; }
        /* BOTONES GRANDES QUE TE GUSTABAN */
        .btn-choice { @apply w-full py-10 rounded-[40px] font-black uppercase text-sm tracking-widest shadow-xl transition-all active:scale-[0.97] flex flex-col items-center justify-center gap-2 border-2 bg-white border-slate-100; }
        .input-premium { @apply w-full p-5 bg-slate-50 border-2 border-transparent rounded-2xl outline-none focus:border-blue-500 focus:bg-white font-bold text-slate-700 transition-all uppercase; }
        .accordion-content { max-height: 0; overflow: hidden; transition: max-height 0.3s ease-out; }
        .accordion-open .accordion-content { max-height: 10000px; }
        .rotate-icon { transition: transform 0.3s; }
        .accordion-open .rotate-icon { transform: rotate(45deg); }
    </style>
</head>
<body class="min-h-screen pb-10">

    <div class="max-w-xl mx-auto min-h-screen flex flex-col relative">
        <header class="bg-slate-900 text-white p-10 pt-14 rounded-b-[50px] shadow-2xl text-center">
            <h1 class="text-4xl font-black italic">BIO-FIX<span class="text-blue-500">®</span></h1>
            <p class="text-[9px] text-slate-400 font-bold uppercase tracking-[0.5em] mt-3">Professional Implant Systems</p>
        </header>

        <nav class="glass sticky top-4 mx-6 mt-[-25px] p-4 rounded-[24px] shadow-xl z-50 flex justify-between items-center border border-white/40">
            <button id="btn-volver" onclick="goBack()" class="w-10 h-10 flex items-center justify-center bg-slate-100 rounded-xl font-black hidden">←</button>
            <div class="flex flex-col ml-2">
                <span id="nav-subtitle" class="text-sm font-black text-slate-900 uppercase italic">Bienvenido</span>
            </div>
            <button onclick="goToResumen()" class="bg-slate-900 text-white px-5 py-3 rounded-xl font-black text-[10px] uppercase">
                Pedido (<span id="cart-count">0</span>)
            </button>
        </nav>

        <main class="p-6 mt-6 flex-grow">
            <section id="step-choice">
                <div class="grid grid-cols-1 gap-5 mt-10">
                    <button onclick="showSection('step-login-old')" class="btn-choice">👨‍⚕️ Cliente Registrado</button>
                    <button onclick="showSection('step-login-new')" class="btn-choice !bg-blue-600 !text-white !border-blue-500">✨ Registro Nuevo</button>
                </div>
            </section>

            <section id="step-login-old" class="hidden space-y-6">
                <div class="bg-white p-8 rounded-[40px] card-shadow border border-slate-100">
                    <input type="text" id="old_nom" placeholder="Nombre y Apellido" class="input-premium mb-4">
                    <input type="text" id="old_dni" placeholder="DNI" class="input-premium">
                </div>
                <button onclick="validateStart('old')" class="w-full bg-slate-900 text-white py-6 rounded-[24px] font-black uppercase">Ingresar</button>
            </section>

            <section id="step-login-new" class="hidden space-y-6">
                <div class="bg-white p-8 rounded-[40px] card-shadow border border-slate-100 space-y-3">
                    <input type="text" id="new_nom" placeholder="Nombre y Apellido *" class="input-premium">
                    <input type="text" id="new_dni" placeholder="DNI *" class="input-premium">
                    <input type="text" id="new_mat" placeholder="Matrícula" class="input-premium">
                </div>
                <button onclick="validateStart('new')" class="w-full bg-blue-600 text-white py-6 rounded-[24px] font-black uppercase">Registrar</button>
            </section>

            <section id="step-menu" class="hidden space-y-4">
                <button onclick="openSub('sub-implantes')" class="btn-choice !py-6 !flex-row !justify-start px-8">📦 Implantes</button>
                <button onclick="openSub('sub-analogicos')" class="btn-choice !py-6 !flex-row !justify-start px-8">🔩 Comp. Analógicos</button>
                <button onclick="openSub('sub-digital')" class="btn-choice !py-6 !flex-row !justify-start px-8 !bg-purple-700 !text-white">🖥️ Flujo Digital</button>
            </section>

            <section id="sub-implantes" class="hidden grid grid-cols-1 gap-4">
                <button onclick="loadProducts('implantes', 'monopieza')" class="btn-choice"><span class="text-blue-600">MONOPIEZA</span> <span class="font-normal text-slate-900 text-xs">MP</span></button>
                <button onclick="loadProducts('implantes', 'basales')" class="btn-choice"><span class="text-blue-600">BASALES</span> <span class="font-normal text-slate-900 text-xs">IB / IBT</span></button>
                <button onclick="loadProducts('implantes', 'compresivos')" class="btn-choice"><span class="text-blue-600">COMPRESIVOS</span> <span class="font-normal text-slate-900 text-xs">CMU</span></button>
                <button onclick="loadProducts('implantes', 'hi')" class="btn-choice"><span class="text-blue-600">HEXÁGONO INTERNO</span> <span class="font-normal text-slate-900 text-xs">HI</span></button>
                <button onclick="loadProducts('implantes', 'he')" class="btn-choice"><span class="text-blue-600">HEXÁGONO EXTERNO</span> <span class="font-normal text-slate-900 text-xs">HE</span></button>
                <button onclick="loadProducts('implantes', 'cmhi')" class="btn-choice"><span class="text-blue-600">CONO MORSE</span> <span class="font-normal text-slate-900 text-xs">CM</span></button>
                <button onclick="loadProducts('implantes', 'mu')" class="btn-choice !border-amber-400"><span class="text-amber-500">SISTEMA MULTIUNIT</span> <span class="font-normal text-slate-900 text-xs">MU</span></button>
            </section>

            <section id="sub-analogicos" class="hidden grid grid-cols-1 gap-4">
                <button onclick="loadProducts('analogicos', 'mp')" class="btn-choice">MONOPIEZA <span class="font-normal text-xs">MP</span></button>
                <button onclick="loadProducts('analogicos', 'cmu')" class="btn-choice">COMPRESIVOS <span class="font-normal text-xs">CMU</span></button>
                <button onclick="loadProducts('analogicos', 'hi')" class="btn-choice">HEXÁGONO INTERNO <span class="font-normal text-xs">HI</span></button>
                <button onclick="loadProducts('analogicos', 'he')" class="btn-choice">HEXÁGONO EXTERNO <span class="font-normal text-xs">HE</span></button>
                <button onclick="loadProducts('analogicos', 'cm')" class="btn-choice">CONO MORSE <span class="font-normal text-xs">CM</span></button>
                <button onclick="loadProducts('analogicos', 'mu_pro')" class="btn-choice !border-amber-400">SISTEMA MULTIUNIT <span class="font-normal text-xs">MU</span></button>
            </section>

            <section id="sub-digital" class="hidden grid grid-cols-1 gap-4">
                <button onclick="loadProducts('digital', 'cmu')" class="btn-choice">SISTEMA CMU</button>
                <button onclick="loadProducts('digital', 'hi')" class="btn-choice">SISTEMA HI</button>
                <button onclick="loadProducts('digital', 'he')" class="btn-choice">SISTEMA HE</button>
                <button onclick="loadProducts('digital', 'cm')" class="btn-choice">SISTEMA CM</button>
            </section>

            <section id="step-lista" class="hidden space-y-4"></section>
            <section id="step-resumen" class="hidden space-y-5"></section>
        </main>
    </div>

    <script>
        // BASE DE DATOS (No se tocó ninguna medida)
        const DB = {
            implantes: {
                monopieza: { "MP Ø3.0": ["MP Ø3.0x6mm","MP Ø3.0x8mm","MP Ø3.0x10mm","MP Ø3.0x11.5mm","MP Ø3.0x13mm","MP Ø3.0x15mm","MP Ø3.0x18mm","MP Ø3.0x20mm"],"MP Ø3.5": ["MP Ø3.5x6mm","MP Ø3.5x8mm","MP Ø3.5x10mm","MP Ø3.5x11.5mm","MP Ø3.5x13mm","MP Ø3.5x15mm","MP Ø3.5x18mm","MP Ø3.5x20mm"],"MP Ø4.0": ["MP Ø4.0x6mm","MP Ø4.0x8mm","MP Ø4.0x10mm","MP Ø4.0x11.5mm","MP Ø4.0x13mm","MP Ø4.0x15mm","MP Ø4.0x18mm","MP Ø4.0x20mm"],"MP Ø4.5": ["MP Ø4.5x6mm","MP Ø4.5x8mm","MP Ø4.5x10mm","MP Ø4.5x11.5mm","MP Ø4.5x13mm","MP Ø4.5x15mm","MP Ø4.5x18mm","MP Ø4.5x20mm"],"MP Ø5.0": ["MP Ø5.0x6mm","MP Ø5.0x8mm","MP Ø5.0x10mm","MP Ø5.0x11.5mm","MP Ø5.0x13mm"],"MP Ø5.5": ["MP Ø5.5x6mm","MP Ø5.5x8mm","MP Ø5.5x10mm","MP Ø5.5x11.5mm","MP Ø5.5x13mm"]},
                basales: { "IB - PULIDO": ["IB Ø3.5x10mm","IB Ø3.5x12mm","IB Ø3.5x14mm","IB Ø3.5x15mm","IB Ø3.5x18mm","IB Ø3.5x21mm","IB Ø3.5x23mm","IB Ø3.5x26mm","IB Ø3.5x28mm","IB Ø3.5x24 C14","IB Ø3.5x26 C16","IB Ø3.5x28 C18","IB Ø4.5x10mm","IB Ø4.5x12mm","IB Ø4.5x15mm","IB Ø4.5x18mm","IB Ø4.5x21mm","IB Ø4.5x23mm","IB Ø4.5x26mm","IB Ø4.5x28mm","IB Ø4.5x24 C14","IB Ø4.5x26 C16","IB Ø4.5x28 C18","IB Ø5.5x9mm","IB Ø5.5x10mm","IB Ø5.5x12mm","IB Ø5.5x15mm","IB Ø5.5x18mm","IB Ø6.5x9mm","IB Ø6.5x10mm","IB Ø6.5x12mm","IB Ø6.5x15mm","IB Ø8.5x9mm","IB Ø8.5x10mm","IB Ø8.5x12mm","IB Ø8.5x15mm"],"IBT - TRATAMIENTO": ["IBT Ø3.5x10mm","IBT Ø3.5x12mm","IBT Ø3.5x14mm","IBT Ø3.5x15mm","IBT Ø3.5x18mm","IBT Ø3.5x21mm","IBT Ø3.5x23mm","IBT Ø3.5x26mm","IBT Ø3.5x28mm","IBT Ø3.5x24 C14","IBT Ø3.5x26 C16","IBT Ø3.5x28 C18","IBT Ø4.5x10mm","IBT Ø4.5x12mm","IBT Ø4.5x15mm","IBT Ø4.5x18mm","IBT Ø4.5x21mm","IBT Ø4.5x23mm","IBT Ø4.5x26mm","IBT Ø4.5x28mm","IBT Ø4.5x24 C14","IBT Ø4.5x26 C16","IBT Ø4.5x28 C18","IBT Ø5.5x9mm","IBT Ø5.5x10mm","IBT Ø5.5x12mm","IBT Ø5.5x15mm","IBT Ø5.5x18mm","IBT Ø6.5x9mm","IBT Ø6.5x10mm","IBT Ø6.5x12mm","IBT Ø6.5x15mm","IBT Ø8.5x9mm","IBT Ø8.5x10mm","IBT Ø8.5x12mm","IBT Ø8.5x15mm"]},
                compresivos: { "SISTEMA CMU (ESTÁNDAR)": ["CMU Ø3.0x6mm","CMU Ø3.0x8mm","CMU Ø3.0x10mm","CMU Ø3.0x11.5mm","CMU Ø3.0x13mm","CMU Ø3.0x15mm","CMU Ø3.0x18mm","CMU Ø3.0x20mm","CMU Ø3.5x6mm","CMU Ø3.5x8mm","CMU Ø3.5x10mm","CMU Ø3.5x11.5mm","CMU Ø3.5x13mm","CMU Ø3.5x15mm","CMU Ø3.5x18mm","CMU Ø3.5x20mm","CMU Ø4.0x6mm","CMU Ø4.0x8mm","CMU Ø4.0x10mm","CMU Ø4.0x11.5mm","CMU Ø4.0x13mm","CMU Ø4.0x15mm","CMU Ø4.0x18mm","CMU Ø4.0x20mm","CMU Ø4.5x6mm","CMU Ø4.5x8mm","CMU Ø4.5x10mm","CMU Ø4.5x11.5mm","CMU Ø4.5x13mm","CMU Ø4.5x15mm","CMU Ø4.5x18mm","CMU Ø4.5x20mm","CMU Ø5.0x6mm","CMU Ø5.0x8mm","CMU Ø5.0x10mm","CMU Ø5.0x11.5mm","CMU Ø5.0x13mm","CMU Ø5.5x6mm","CMU Ø5.5x8mm","CMU Ø5.5x10mm","CMU Ø5.5x11.5mm","CMU Ø5.5x13mm"],"SISTEMA CMU (C3)": ["CMU Ø3.0x6mm C3","CMU Ø3.0x8mm C3","CMU Ø3.0x10mm C3","CMU Ø3.0x11.5mm C3","CMU Ø3.0x13mm C3","CMU Ø3.0x15mm C3","CMU Ø3.0x18mm C3","CMU Ø3.0x20mm C3","CMU Ø3.5x6mm C3","CMU Ø3.5x8mm C3","CMU Ø3.5x10mm C3","CMU Ø3.5x11.5mm C3","CMU Ø3.5x13mm C3","CMU Ø3.5x15mm C3","CMU Ø3.5x18mm C3","CMU Ø3.5x20mm C3","CMU Ø4.0x6mm C3","CMU Ø4.0x8mm C3","CMU Ø4.0x10mm C3","CMU Ø4.0x11.5mm C3","CMU Ø4.0x13mm C3","CMU Ø4.0x15mm C3","CMU Ø4.0x18mm C3","CMU Ø4.0x20mm C3","CMU Ø4.5x6mm C3","CMU Ø4.5x8mm C3","CMU Ø4.5x10mm C3","CMU Ø4.5x11.5mm C3","CMU Ø4.5x13mm C3","CMU Ø4.5x15mm C3","CMU Ø4.5x18mm C3","CMU Ø4.5x20mm C3","CMU Ø5.0x6mm C3","CMU Ø5.0x8mm C3","CMU Ø5.0x10mm C3","CMU Ø5.0x11.5mm C3","CMU Ø5.0x13mm C3","CMU Ø5.5x6mm C3","CMU Ø5.5x8mm C3","CMU Ø5.5x10mm C3","CMU Ø5.5x11.5mm C3","CMU Ø5.5x13mm C3"]},
                hi: { "HEX INTERNO": ["HI Ø3.30x6.5mm","HI Ø3.30x8.0mm","HI Ø3.30x10mm","HI Ø3.30x11.5mm","HI Ø3.30x13mm","HI Ø3.30x16mm","HI Ø3.75x6.5mm","HI Ø3.75x8.0mm","HI Ø3.75x10mm","HI Ø3.75x11.5mm","HI Ø3.75x13mm","HI Ø3.75x16mm","HI Ø4.2x6.5mm","HI Ø4.2x8.0mm","HI Ø4.2x10mm","HI Ø4.2x11.5mm","HI Ø4.2x13mm","HI Ø4.2x16mm","HI Ø5.0x6.5mm","HI Ø5.0x8.0mm","HI Ø5.0x10mm","HI Ø5.0x11.5mm","HI Ø5.0x13mm","HI Ø5.0x16mm"]},
                he: { "HE Ø3.30 (Plat. 3.4)": ["HE Ø3.30x8.5mm","HE Ø3.30x10mm","HE Ø3.30x11.5mm","HE Ø3.30x13mm","HE Ø3.30x15mm"],"HE Ø3.75 (Plat. 4.1)": ["HE Ø3.75x8mm","HE Ø3.75x10mm","HE Ø3.75x11.5mm","HE Ø3.75x13mm","HE Ø3.75x15mm"],"HE Ø4.0 (Plat. 4.1)": ["HE Ø4.0x6mm","HE Ø4.0x8.5mm","HE Ø4.0x10mm","HE Ø4.0x11.5mm","HE Ø4.0x13mm","HE Ø4.0x15mm"],"HE Ø5.0 (Plat. 5.0)": ["HE Ø5.0x6mm","HE Ø5.0x8.5mm","HE Ø5.0x10mm","HE Ø5.0x11.5mm","HE Ø5.0x13mm","HE Ø5.0x15mm"]},
                cmhi: { "CONO MORSE": ["CMHI Ø3.30x8mm","CMHI Ø3.30x10mm","CMHI Ø3.30x11.5mm","CMHI Ø3.30x13mm","CMHI Ø3.30x16mm","CMHI Ø3.75x8mm","CMHI Ø3.75x10mm","CMHI Ø3.75x11.5mm","CMHI Ø3.75x13mm","CMHI Ø3.75x16mm","CMHI Ø4.20x8mm","CMHI Ø4.20x10mm","CMHI Ø4.20x11.5mm","CMHI Ø4.20x13mm","CMHI Ø4.20x16mm","CMHI Ø5.0x8mm","CMHI Ø5.0x10mm","CMHI Ø5.0x11.5mm","CMHI Ø5.0x13mm","CMHI Ø5.0x16mm"]},
                mu: {
                    "PILARES MU CM": ["Minipilar Altura 0,8 - Cono Morse","Minipilar Altura 1,5 - Cono Morse","Minipilar Altura 2,5 - Cono Morse","Minipilar Altura 3,5 - Cono Morse","Minipilar Altura 4,5 - Cono Morse"],
                    "PILARES MU HI": ["Minipilar Altura 1 - Hexágono Interno","Minipilar Altura 2 - Hexágono Interno","Minipilar Altura 3 - Hexágono Interno","Minipilar Altura 4 - Hexágono Interno"],
                    "PILARES MU HE": ["Minipilar Altura 1 - Hexágono Externo","Minipilar Altura 2 - Hexágono Externo","Minipilar Altura 3 - Hexágono Externo","Minipilar Altura 4 - Hexágono Externo"]
                }
            },
            analogicos: {
                mp: { "COMPONENTES MP": ["UCLA rotacional para Implantes MonoPieza","Analogo Plastico Rotacional de implante Monopieza","Transfer plastico rotacional para implantes Monopieza"] },
                cmu: { "CICATRIZALES CMU": ["Cicatrizal Altura de 2mm - Compresivo Multi Unit","Cicatrizal Altura de 3mm - Compresivo Multi Unit","Cicatrizal Altura de 4mm - Compresivo Multi Unit"],"PROTESIS CMU": ["Ball Attach Altura (h)2mm - Compresivo Multi Unit","Ball Attach Altura (h)3mm - Compresivo Multi Unit","Pilar Recto Hombro 1 - Compresivo Multi Unit","Tornillo M2 para implante Compresivo Multi Unit"]},
                hi: { "CICATRIZALES HI": ["Cicatrizal Altura 1mm -Hexágono Interno","Cicatrizal Altura 2mm -Hexágono Interno","Cicatrizal Altura 3mm -Hexágono Interno","Cicatrizal Altura 4mm -Hexágono Interno"],"BALL ATTACH HI": ["Ball attach y cazoleta con O'ring Altura 1 - Hexágono Interno","Ball attach y cazoleta con O'ring Altura 2 - Hexágono Interno","Ball attach y cazoleta con O'ring Altura 3 - Hexágono Interno","Ball attach y cazoleta con O'ring Altura 4 - Hexágono Interno"]},
                he: { "TORNILLOS Y ANÁLOGOS HE": ["Análogo - HE 3.4","Análogo - HE 4.1","Análogo - HE 5.0"],"CICATRIZALES HE": ["Cicatrizal Altura 1 - HE Ø3.4","Cicatrizal Altura 1 - HE Ø4.1","Cicatrizal Altura 1 - HE Ø5.0"]},
                cm: { "CICATRIZALES CM": ["Pilar de Cicatrización CM 3,3 x 1,5","Pilar de Cicatrización CM 3,3 x 2,5","Pilar de Cicatrización CM 4,5 x 1,5","Pilar de Cicatrización CM 4,5 x 2,5"]},
                mu_pro: { "ACCESORIOS MU": ["Pilar Rotacional c/microtornillo - MU", "Pilar Anti-rotacional c/microtornillo - MU", "Ucla calcinable rotacional c/microtornillo - MU", "Tapón de cierre plástico c/microtornillo - MU", "Transfer cubeta abierta c/microtornillo - MU", "Transfer cubeta Cerrada c/microtornillo - MU", "Análogo de Minipilar"] }
            },
            digital: {
                cmu: { "COMPONENTES": ["Cuerpo de escaneo y tornillo M2 P/Implante CMU", "Ti-Base y tornillo m2 - CMU", "Tornillo M2 para implante CMU"] },
                hi: { "COMPONENTES": ["Análogo digital - HI","Cuerpo de escaneo - HI","Ti Base Anti-Rotacional y tornillo M1.8 - HI"] },
                he: { "COMPONENTES": ["Análogo digital - HE 4.1","Cuerpo de escaneo - HE 4.1","Ti Base Anti-Rotacional - HE 4.1"] },
                cm: { 
                    "PLATAFORMA 3.3": ["Análogo Digital - CM 3.3", "Cuerpo de Escaneo y tornillo - CM 3.3", "T-Base 3,3x1x4 CM","T-Base 3,3x2x4 CM","T-Base 3,3x3x4 CM"],
                    "PLATAFORMA 4.5": ["Análogo Digital - CM 4.5", "Cuerpo de Escaneo y tornillo - CM 4.5", "T-Base 4,5x1x4 CM","T-Base 4,5x2x4 CM","T-Base 4,5x3x4 CM"]
                }
            }
        };

        let cart = {}; let stack = ['step-choice']; let clientData = {};
        function showSection(id, push = true) {
            document.querySelectorAll('section').forEach(s => s.classList.add('hidden'));
            document.getElementById(id).classList.remove('hidden');
            if(push) stack.push(id);
            document.getElementById('btn-volver').classList.toggle('hidden', stack.length <= 1);
            window.scrollTo(0,0);
        }
        function goBack() { if(stack.length > 1) { stack.pop(); showSection(stack.pop()); } }
        function validateStart(type) {
            const nom = type === 'old' ? document.getElementById('old_nom').value : document.getElementById('new_nom').value;
            if(!nom) return alert("Ingrese su nombre");
            clientData = { nombre: nom };
            showSection('step-menu');
        }
        function openSub(id) { showSection(id); }
        function loadProducts(cat, subcat) {
            showSection('step-lista');
            const container = document.getElementById('step-lista');
            container.innerHTML = "";
            const data = DB[cat][subcat];
            for (const group in data) {
                const groupDiv = document.createElement('div');
                groupDiv.className = "bg-white rounded-[32px] overflow-hidden card-shadow mb-4";
                let html = `<button onclick="this.parentElement.classList.toggle('accordion-open')" class="w-full flex justify-between items-center p-6 bg-slate-900 text-white font-black text-[10px] uppercase">
                    <span>${group}</span><span class="text-xl rotate-icon">+</span></button><div class="accordion-content divide-y">`;
                data[group].forEach(item => {
                    const q = cart[item] || 0;
                    html += `<div class="flex justify-between items-center p-6"><span class="text-[10px] font-black text-slate-600 uppercase pr-4">${item}</span>
                        <div class="flex items-center gap-3 bg-slate-100 p-1 rounded-2xl">
                            <button onclick="update('${item}',-1,this)" class="w-10 h-10 bg-white rounded-xl shadow font-bold">-</button>
                            <span class="font-black text-sm w-4 text-center">${q}</span>
                            <button onclick="update('${item}',1,this)" class="w-10 h-10 bg-slate-900 text-white rounded-xl shadow font-bold">+</button>
                        </div></div>`;
                });
                groupDiv.innerHTML = html + "</div>";
                container.appendChild(groupDiv);
            }
        }
        function update(item, delta, btn) {
            cart[item] = (cart[item] || 0) + delta;
            if(cart[item] <= 0) delete cart[item];
            btn.parentElement.querySelector('span').innerText = cart[item] || 0;
            document.getElementById('cart-count').innerText = Object.values(cart).reduce((a,b)=>a+b, 0);
        }
        function goToResumen() {
            showSection('step-resumen');
            const container = document.getElementById('step-resumen');
            container.innerHTML = `<h2 class="font-black uppercase text-center mb-6">Resumen de Pedido</h2><div class="bg-blue-50 p-4 rounded-2xl mb-4 font-bold text-xs">Dr/a: ${clientData.nombre}</div>`;
            Object.entries(cart).forEach(([n, q]) => {
                container.innerHTML += `<div class="p-6 bg-white rounded-3xl mb-2 flex justify-between border"><span>${n}</span><b>x${q}</b></div>`;
            });
            container.innerHTML += `<button onclick="sendWA()" class="w-full bg-green-600 text-white py-6 rounded-3xl mt-6 font-black uppercase">Enviar Pedido</button>`;
        }
        function sendWA() {
            let m = `*PEDIDO BIO-FIX®*\n*DR/A:* ${clientData.nombre}\n\n`;
            Object.entries(cart).forEach(([n,q])=> m+=`✅ ${q} x ${n}\n`);
            window.open(`https://wa.me/5491122334455?text=${encodeURIComponent(m)}`);
        }
    </script>
</body>
</html>
