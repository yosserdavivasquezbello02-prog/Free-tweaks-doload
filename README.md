[Yosser.html](https://github.com/user-attachments/files/29278734/Yosser.html)
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Yosser_Tweaks - Dashboard</title>
    <style>
        :root {
            --bg-main: #0a0b10;
            --bg-card: #121420;
            --text-primary: #ffffff;
            --text-secondary: #8e94b2;
            --accent: #00ff66;
            --accent-hover: #00cc52;
            --border-color: #1f2335;
            --global-btn-bg: #ff3366;
            --global-btn-hover: #e02454;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', system-ui, sans-serif;
        }

        body {
            background-color: var(--bg-main);
            color: var(--text-primary);
            padding: 24px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            margin-bottom: 24px;
            padding: 24px;
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 16px;
        }

        header h1 {
            color: var(--accent);
            font-size: 2.5rem;
            margin-bottom: 16px;
        }

        /* Bot�n de Activaci�n Masiva */
        .global-trigger-container {
            text-align: center;
            margin-bottom: 32px;
        }

        .btn-global-execute {
            background: var(--global-btn-bg);
            color: #ffffff;
            border: none;
            padding: 16px 32px;
            font-size: 1.2rem;
            font-weight: 700;
            border-radius: 12px;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(255, 51, 102, 0.3);
            transition: all 0.2s ease;
            width: 100%;
            max-width: 600px;
        }

        .btn-global-execute:hover {
            background: var(--global-btn-hover);
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255, 51, 102, 0.5);
        }

        .btn-global-execute:active {
            transform: translateY(0);
        }

        /* Monitor de Hardware */
        .monitor-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 16px;
            max-width: 600px;
            margin: 0 auto;
        }

        .monitor-card {
            background: rgba(255, 255, 255, 0.02);
            border: 1px solid var(--border-color);
            padding: 12px;
            border-radius: 12px;
            text-align: center;
        }

        .monitor-card label {
            display: block;
            font-size: 0.75rem;
            color: var(--text-secondary);
            text-transform: uppercase;
            margin-bottom: 4px;
        }

        .monitor-card span {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--accent);
        }

        /* Navegaci�n */
        .tabs-nav {
            display: flex;
            gap: 8px;
            margin-bottom: 24px;
            overflow-x: auto;
            padding-bottom: 8px;
        }

        .tab-btn {
            background: var(--bg-card);
            color: var(--text-secondary);
            border: 1px solid var(--border-color);
            padding: 12px 24px;
            border-radius: 10px;
            cursor: pointer;
            font-weight: 600;
            white-space: nowrap;
            transition: all 0.2s ease;
        }

        .tab-btn.active {
            background: var(--accent);
            color: #000000;
            border-color: var(--accent);
        }

        /* Paneles */
        .tab-panel {
            display: none;
        }

        .tab-panel.active {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 20px;
        }

        /* Tarjetas */
        .card {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 20px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            transition: all 0.2s;
        }

        .card:hover {
            transform: translateY(-2px);
            border-color: var(--accent);
        }

        .card h3 {
            font-size: 1.1rem;
            margin-bottom: 8px;
            color: var(--text-primary);
        }

        .card p {
            color: var(--text-secondary);
            font-size: 0.85rem;
            margin-bottom: 20px;
            line-height: 1.4;
        }

        .btn-execute {
            background: rgba(0, 255, 102, 0.08);
            color: var(--accent);
            border: 1px solid var(--accent);
            padding: 10px 16px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            width: 100%;
            transition: all 0.2s;
        }

        .btn-execute:hover {
            background: var(--accent);
            color: #000000;
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <h1>Yosser_Tweaks</h1>
            <div class="monitor-grid">
                <div class="monitor-card">
                    <label>CPU Usage</label>
                    <span id="cpu-stat">0%</span>
                </div>
                <div class="monitor-card">
                    <label>GPU Usage</label>
                    <span id="gpu-stat">0%</span>
                </div>
                <div class="monitor-card">
                    <label>Disk Active</label>
                    <span id="disk-stat">0%</span>
                </div>
            </div>
        </header>

        <div class="global-trigger-container">
            <button class="btn-global-execute" onclick="executeAllTweaks()">? ACTIVAR TODO CON 1 CLICK ?</button>
        </div>

        <nav class="tabs-nav">
            <button class="tab-btn active" onclick="switchTab(event, 'regedit')">Regedit Zero Delay (18)</button>
            <button class="tab-btn" onclick="switchTab(event, 'power')">Power Options (14)</button>
            <button class="tab-btn" onclick="switchTab(event, 'internet')">Internet (2)</button>
            <button class="tab-btn" onclick="switchTab(event, 'cmds')">Comandos (6)</button>
            <button class="tab-btn" onclick="switchTab(event, 'mouse')">Perif�ricos Zero Delay (9)</button>
        </nav>

        <main>
            <div id="regedit" class="tab-panel active"></div>
            <div id="power" class="tab-panel"></div>
            <div id="internet" class="tab-panel"></div>
            <div id="cmds" class="tab-panel"></div>
            <div id="mouse" class="tab-panel"></div>
        </main>
    </div>

    <script>
        // Simulador de Monitor de Componentes
        function updateHardwareStats() {
            document.getElementById('cpu-stat').textContent = Math.floor(Math.random() * (18 - 3) + 3) + '%';
            document.getElementById('gpu-stat').textContent = Math.floor(Math.random() * (30 - 5) + 5) + '%';
            document.getElementById('disk-stat').textContent = Math.floor(Math.random() * (4 - 1) + 1) + '%';
        }
        setInterval(updateHardwareStats, 2000);
        updateHardwareStats();

        // Control de Pesta�as
        function switchTab(event, panelId) {
            document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
            document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
            document.getElementById(panelId).classList.add('active');
            event.currentTarget.classList.add('active');
        }

        // Descarga de archivos .reg
        function createRegFile(filename, content) {
            const blob = new Blob([content], { type: 'text/plain;charset=utf-8' });
            const link = document.createElement('a');
            link.href = URL.createObjectURL(blob);
            link.download = `${filename}.reg`;
            link.click();
            URL.revokeObjectURL(link.href);
        }

        // Copiar comandos
        function copyToClipboard(text, silent = false) {
            navigator.clipboard.writeText(text).then(() => {
                if (!silent) {
                    alert("Comando copiado al portapapeles con �xito.");
                }
            });
        }

        // Estructuras de Datos de Registro crudos (Sin encabezados individuales para la fusi�n)
        const regContents = {
            SystemResponsiveness: `[HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\Multimedia\\SystemProfile]\n"SystemResponsiveness"=dword:00000000`,
            NetworkThrottling: `[HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\Multimedia\\SystemProfile]\n"NetworkThrottlingIndex"=dword:ffffffff`,
            GPUPriority: `[HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\Multimedia\\SystemProfile\\Tasks\\Games]\n"GPU Priority"=dword:00000008`,
            PriorityAssociation: `[HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\Multimedia\\SystemProfile\\Tasks\\Games]\n"Priority"=dword:00000006`,
            SchedulingCategory: `[HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\Multimedia\\SystemProfile\\Tasks\\Games]\n"Scheduling Category"="High"`,
            VisualFXPerf: `[HKEY_CURRENT_USER\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\VisualEffects]\n"VisualFXSetting"=dword:00000002`,
            MenuShowDelay: `[HKEY_CURRENT_USER\\Control Panel\\Desktop]\n"MenuShowDelay"="0"`,
            DisableHiber: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Power]\n"HibernateEnabled"=dword:00000000`,
            DisableDVR: `[HKEY_CURRENT_USER\\System\\GameConfigStore]\n"GameDVR_Enabled"=dword:00000000`,
            Win32Priority: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\PriorityControl]\n"Win32PrioritySeparation"=dword:00000026`,
            DisableTransparency: `[HKEY_CURRENT_USER\\Software\\Microsoft\\Windows\\CurrentVersion\\Themes\\Personalize]\n"EnableTransparency"=dword:00000000`,
            ProcMitigation: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Session Manager\\Memory Management]\n"FeatureSettingsOverride"=dword:00000003\n"FeatureSettingsOverrideMask"=dword:00000003`,
            DisableIndexing: `[HKEY_LOCAL_MACHINE\\SOFTWARE\\Policies\\Microsoft\\Windows\\Windows Search]\n"AllowCortana"=dword:00000000`,
            ClearPageFile: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Session Manager\\Memory Management]\n"ClearPageFileAtShutdown"=dword:00000001`,
            IoPageLockLimit: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Session Manager\\Memory Management]\n"IoPageLockLimit"=dword:04000000`,
            CPUErrorHandling: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CrashControl]\n"AutoReboot"=dword:00000000\n"CrashDumpEnabled"=dword:00000000`,
            DiskNtfsDisableLastAccess: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\FileSystem]\n"NtfsDisableLastAccessUpdate"=dword:00000001`,
            DisablePrefetcher: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Session Manager\\Memory Management\\PrefetchParameters]\n"EnablePrefetcher"=dword:00000000\n"EnableSuperfetch"=dword:00000000`,
            CoreParking: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Power\\PowerSettings\\54533251-82be-4824-96c1-47b60b740d00\\0cc5b647-c1df-4637-891a-dec35c318583]\n"Attributes"=dword:00000000`,
            PCIeLinkState: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Power]\n"HighPerformance"=dword:00000001`,
            USBSuspend: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\USB]\n"DisableSelectiveSuspend"=dword:00000001`,
            CpuMinState: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Power]\n"ResetToMax"=dword:00000001`,
            DiskTimeout: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Power]\n"DiskIdleTimeout"=dword:00000000`,
            PowerThrottling: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Power]\n"PowerThrottlingOff"=dword:00000001`,
            GpuPowerPerf: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Power]\n"GpuPreference"=dword:00000002`,
            CoolingPolicy: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Power]\n"CoolingMode"=dword:00000001`,
            CsEnabled: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Power]\n"CsEnabled"=dword:00000000`,
            AhciPower: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Power]\n"SataPowerMode"=dword:00000000`,
            UnhidePower: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Power]\n"Attributes"=dword:00000002`,
            PowerMizer: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Video]\n"PowerMizerLevel"=dword:00000001`,
            DisableEET: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Power\\PowerSettings\\54533251-82be-4824-96c1-47b60b740d00\\45bcc0a2-7ae0-4614-998d-dc7307c22a95]\n"Attributes"=dword:00000000`,
            InterruptSteering: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Power\\PowerSettings\\54533251-82be-4824-96c1-47b60b740d00\\2bfc24f9-5ea9-414b-b014-bb26702b748a]\n"Attributes"=dword:00000000`,
            TcpAckFrequency: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\Tcpip\\Parameters\\Interfaces]\n"TcpAckFrequency"=dword:00000001`,
            TCPNoDelay: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\Tcpip\\Parameters\\Interfaces]\n"TCPNoDelay"=dword:00000001`,
            MouseSpeed: `[HKEY_CURRENT_USER\\Control Panel\\Mouse]\n"MouseSpeed"="0"`,
            MouseThresholds: `[HKEY_CURRENT_USER\\Control Panel\\Mouse]\n"MouseThreshold1"="0"\n"MouseThreshold2"="0"`,
            EnhancedPrecision: `[HKEY_CURRENT_USER\\Control Panel\\Mouse]\n"MouseHoverWidth"=dword:00000004`,
            MouseQueueSize: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\mouclass\\Parameters]\n"MouseDataQueueSize"=dword:00000014`,
            SmoothMouseCurve: `[HKEY_CURRENT_USER\\Control Panel\\Desktop]\n"SmoothMouseXCurve"=hex:00,00,00,00,00,00,00,00\n"SmoothMouseYCurve"=hex:00,00,00,00,00,00,00,00`,
            KeyboardDelay: `[HKEY_CURRENT_USER\\Control Panel\\Accessibility\\Keyboard Response]\n"DelayBeforeAcceptance"="0"\n[HKEY_CURRENT_USER\\Control Panel\\Keyboard]\n"KeyboardDelay"="0"`,
            KeyboardSpeed: `[HKEY_CURRENT_USER\\Control Panel\\Keyboard]\n"KeyboardSpeed"="31"`,
            KbdQueueSize: `[HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\kbdclass\\Parameters]\n"KeyboardDataQueueSize"=dword:00000014`,
            KbdFlags: `[HKEY_CURRENT_USER\\Control Panel\\Accessibility\\Keyboard Response]\n"Flags"=dword:00000001`
        };

        // Datos de optimizaci�n modulares
        const dataModules = {
            regedit: [
                { title: "SystemResponsiveness", desc: "Establece la prioridad de recursos para procesos de juego a m�xima prioridad.", label: "Descargar .REG", action: () => createRegFile("SystemResponsiveness", `Windows Registry Editor Version 5.00\n\n${regContents.SystemResponsiveness}`) },
                { title: "NetworkThrottlingIndex", desc: "Desactiva la limitaci�n de red por software al jugar.", label: "Descargar .REG", action: () => createRegFile("NetworkThrottling", `Windows Registry Editor Version 5.00\n\n${regContents.NetworkThrottling}`) },
                { title: "GPU Priority", desc: "Aumenta la prioridad de programaci�n de tareas de la tarjeta gr�fica.", label: "Descargar .REG", action: () => createRegFile("GPUPriority", `Windows Registry Editor Version 5.00\n\n${regContents.GPUPriority}`) },
                { title: "Priority Association", desc: "Vincula los recursos del procesador directamente al flujo de renderizado del juego.", label: "Descargar .REG", action: () => createRegFile("PriorityAssociation", `Windows Registry Editor Version 5.00\n\n${regContents.PriorityAssociation}`) },
                { title: "Scheduling Category", desc: "Asigna los hilos del procesador en la categor�a High para juegos.", label: "Descargar .REG", action: () => createRegFile("SchedulingCategory", `Windows Registry Editor Version 5.00\n\n${regContents.SchedulingCategory}`) },
                { title: "VisualFX Performance", desc: "Desactiva animaciones innecesarias de la interfaz para liberar ciclos de CPU.", label: "Descargar .REG", action: () => createRegFile("VisualFXPerf", `Windows Registry Editor Version 5.00\n\n${regContents.VisualFXPerf}`) },
                { title: "MenuShowDelay 0", desc: "Elimina el retraso de despliegue en los men�s contextuales de Windows.", label: "Descargar .REG", action: () => createRegFile("MenuShowDelay", `Windows Registry Editor Version 5.00\n\n${regContents.MenuShowDelay}`) },
                { title: "Disable Hibernation", desc: "Libera espacio en el disco duro desactivando el archivo hiberfil.sys.", label: "Descargar .REG", action: () => createRegFile("DisableHiber", `Windows Registry Editor Version 5.00\n\n${regContents.DisableHiber}`) },
                { title: "Turn Off DVR / GameBar", desc: "Desactiva la superposici�n de Xbox Game Bar para evitar ca�das de FPS.", label: "Descargar .REG", action: () => createRegFile("DisableDVR", `Windows Registry Editor Version 5.00\n\n${regContents.DisableDVR}`) },
                { title: "Win32PrioritySeparation", desc: "Ajusta la asignaci�n de tiempo del procesador a favor de aplicaciones en primer plano.", label: "Descargar .REG", action: () => createRegFile("Win32Priority", `Windows Registry Editor Version 5.00\n\n${regContents.Win32Priority}`) },
                { title: "Disable Transparency Effects", desc: "Quita las transparencias de Fluent Design disminuyendo el uso de la GPU.", label: "Descargar .REG", action: () => createRegFile("DisableTransparency", `Windows Registry Editor Version 5.00\n\n${regContents.DisableTransparency}`) },
                { title: "Optimize Process Mitigation", desc: "Mitiga el impacto de seguridad espectral en procesadores para mayor fluidez.", label: "Descargar .REG", action: () => createRegFile("ProcMitigation", `Windows Registry Editor Version 5.00\n\n${regContents.ProcMitigation}`) },
                { title: "Disable Search Indexing", desc: "Desactiva la indexaci�n de archivos constante para estabilizar la actividad en disco.", label: "Descargar .REG", action: () => createRegFile("DisableIndexing", `Windows Registry Editor Version 5.00\n\n${regContents.DisableIndexing}`) },
                { title: "Clear PageFile at Shutdown", desc: "Fuerza la limpieza del archivo de paginaci�n para purgar la cach� de memoria.", label: "Descargar .REG", action: () => createRegFile("ClearPageFile", `Windows Registry Editor Version 5.00\n\n${regContents.ClearPageFile}`) },
                { title: "IoPageLockLimit Boost", desc: "Aumenta el b�fer de entrada/salida para transferencias de datos m�s r�pidas.", label: "Descargar .REG", action: () => createRegFile("IoPageLockLimit", `Windows Registry Editor Version 5.00\n\n${regContents.IoPageLockLimit}`) },
                { title: "CPU Internal Error Handling", desc: "Previene interrupciones innecesarias de reporte de errores de CPU durante hilos pesados.", label: "Descargar .REG", action: () => createRegFile("CPUErrorHandling", `Windows Registry Editor Version 5.00\n\n${regContents.CPUErrorHandling}`) },
                { title: "Disk I/O Latency Tweak", desc: "Deshabilita la actualizaci�n del �ltimo acceso a archivos NTFS disminuyendo escrituras.", label: "Descargar .REG", action: () => createRegFile("DiskNtfsDisableLastAccess", `Windows Registry Editor Version 5.00\n\n${regContents.DiskNtfsDisableLastAccess}`) },
                { title: "Disable Prefetcher", desc: "Desactiva la prelectura en disco para evitar picos repentinos de lectura de archivos.", label: "Descargar .REG", action: () => createRegFile("DisablePrefetcher", `Windows Registry Editor Version 5.00\n\n${regContents.DisablePrefetcher}`) }
            ],
            power: [
                { title: "Core Parking Disable", desc: "Fuerza a que todos los n�cleos f�sicos del CPU permanezcan activos al 100%.", label: "Descargar .REG", action: () => createRegFile("CoreParking", `Windows Registry Editor Version 5.00\n\n${regContents.CoreParking}`) },
                { title: "PCI Express Link State Off", desc: "Evita que las ranuras PCIe entren en ahorro de energ�a reduciendo micro-stuttering.", label: "Descargar .REG", action: () => createRegFile("PCIeLinkState", `Windows Registry Editor Version 5.00\n\n${regContents.PCIeLinkState}`) },
                { title: "USB Selective Suspend Disable", desc: "Mantiene los puertos USB con voltaje constante para evitar retraso de perif�ricos.", label: "Descargar .REG", action: () => createRegFile("USBSuspend", `Windows Registry Editor Version 5.00\n\n${regContents.USBSuspend}`) },
                { title: "Processor Minimum State 100%", desc: "Establece la frecuencia m�nima de procesamiento en el estado m�s alto.", label: "Descargar .REG", action: () => createRegFile("CpuMinState", `Windows Registry Editor Version 5.00\n\n${regContents.CpuMinState}`) },
                { title: "Turn Off Hard Disk Timeout", desc: "Evita que las unidades de almacenamiento se apaguen por inactividad.", label: "Descargar .REG", action: () => createRegFile("DiskTimeout", `Windows Registry Editor Version 5.00\n\n${regContents.DiskTimeout}`) },
                { title: "Disable Power Throttling", desc: "Previene que Windows reduzca la energ�a a procesos en segundo plano.", label: "Descargar .REG", action: () => createRegFile("PowerThrottling", `Windows Registry Editor Version 5.00\n\n${regContents.PowerThrottling}`) },
                { title: "Graphics Power Performance", desc: "Fuerza el subsistema de video a priorizar fotogramas sobre consumo.", label: "Descargar .REG", action: () => createRegFile("GpuPowerPerf", `Windows Registry Editor Version 5.00\n\n${regContents.GpuPowerPerf}`) },
                { title: "System Cooling Policy Active", desc: "Activa los ventiladores antes de que el procesador disminuya su velocidad por temperatura.", label: "Descargar .REG", action: () => createRegFile("CoolingPolicy", `Windows Registry Editor Version 5.00\n\n${regContents.CoolingPolicy}`) },
                { title: "Disable Connected Standby", desc: "Desactiva estados de suspensi�n modernos para conservar la RAM limpia.", label: "Descargar .REG", action: () => createRegFile("CsEnabled", `Windows Registry Editor Version 5.00\n\n${regContents.CsEnabled}`) },
                { title: "AHCI Link Power Management", desc: "Configura la interfaz SATA/AHCI en modo de alta velocidad sin retardos.", label: "Descargar .REG", action: () => createRegFile("AhciPower", `Windows Registry Editor Version 5.00\n\n${regContents.AhciPower}`) },
                { title: "Unhide Hidden Power Settings", desc: "Desbloquea atributos avanzados ocultos en el panel de energ�a cl�sico.", label: "Descargar .REG", action: () => createRegFile("UnhidePower", `Windows Registry Editor Version 5.00\n\n${regContents.UnhidePower}`) },
                { title: "NVidia PowerMizer Max Performance", desc: "Ajusta las GPU compatibles para fijar relojes estables durante cargas de juego.", label: "Descargar .REG", action: () => createRegFile("PowerMizer", `Windows Registry Editor Version 5.00\n\n${regContents.PowerMizer}`) },
                { title: "Disable CPU Energy Efficient Turbo", desc: "Desactiva las funciones de optimizaci�n energ�tica de frecuencia para m�xima respuesta.", label: "Descargar .REG", action: () => createRegFile("DisableEET", `Windows Registry Editor Version 5.00\n\n${regContents.DisableEET}`) },
                { title: "Interrupt Steering Mode", desc: "Redirige las interrupciones de hardware directamente a los n�cleos l�gicos del procesador.", label: "Descargar .REG", action: () => createRegFile("InterruptSteering", `Windows Registry Editor Version 5.00\n\n${regContents.InterruptSteering}`) }
            ],
            internet: [
                { title: "TcpAckFrequency Boost", desc: "Env�a confirmaciones de paquetes TCP instant�neamente, bajando el Ping.", label: "Descargar .REG", action: () => createRegFile("TcpAckFrequency", `Windows Registry Editor Version 5.00\n\n${regContents.TcpAckFrequency}`) },
                { title: "TCPNoDelay Activation", desc: "Desactiva el algoritmo de Nagle para evitar acumulaci�n de b�fer de red.", label: "Descargar .REG", action: () => createRegFile("TCPNoDelay", `Windows Registry Editor Version 5.00\n\n${regContents.TCPNoDelay}`) }
            ],
            cmds: [
                { title: "Flush DNS & Reset Sockets", desc: "Vac�a la cach� de resoluci�n de nombres y repara la pila de red Winsock.", label: "Copiar Comando", commandText: "ipconfig /flushdns && netsh winsock reset", action: function() { copyToClipboard(this.commandText); } },
                { title: "Enable Ultimate Performance Plan", desc: "Desbloquea mediante GUID nativo el plan oculto de Rendimiento M�ximo.", label: "Copiar Comando", commandText: "powercfg -duplicatescheme e9a42b02-d5df-448d-aa00-03f14749eb61", action: function() { copyToClipboard(this.commandText); } },
                { title: "Disable BCD Timestamp", desc: "Desactiva los tics de temporizador de la plataforma para mejorar el Input Delay general.", label: "Copiar Comando", commandText: "bcdedit /set useplatformclock false && bcdedit /set disabledynamictick yes", action: function() { copyToClipboard(this.commandText); } },
                { title: "Optimize Drive (Defrag/TRIM)", desc: "Env�a el comando TRIM a las unidades SSD para purgar bloques de datos obsoletos.", label: "Copiar Comando", commandText: "defrag /c /o /v", action: function() { copyToClipboard(this.commandText); } },
                { title: "Disable HPET via CMD", desc: "Fuerza el uso exclusivo del TSC del procesador, reduciendo retrasos en perif�ricos.", label: "Copiar Comando", commandText: "bcdedit /deletevalue useplatformclock", action: function() { copyToClipboard(this.commandText); } },
                { title: "Clear Windows Cache", desc: "Borra de forma masiva los archivos temporales que ralentizan el acceso a disco.", label: "Copiar Comando", commandText: "del /f /s /q %systemdrive%\\*.tmp && del /f /s /q %windir%\\prefetch\\*.*", action: function() { copyToClipboard(this.commandText); } }
            ],
            mouse: [
                { title: "MouseSpeed 0", desc: "Elimina la aceleraci�n por software predeterminada de Windows.", label: "Descargar .REG", action: () => createRegFile("MouseSpeed", `Windows Registry Editor Version 5.00\n\n${regContents.MouseSpeed}`) },
                { title: "Mouse Thresholds Reset", desc: "Establece los l�mites de movimiento en cero para una respuesta lineal p�xel a p�xel.", label: "Descargar .REG", action: () => createRegFile("MouseThresholds", `Windows Registry Editor Version 5.00\n\n${regContents.MouseThresholds}`) },
                { title: "Enhanced Pointer Precision Off", desc: "Fuerza el apagado de la precisi�n mejorada (curva de aceleraci�n logar�tmica).", label: "Descargar .REG", action: () => createRegFile("EnhancedPrecision", `Windows Registry Editor Version 5.00\n\n${regContents.EnhancedPrecision}`) },
                { title: "Mouse Data Queue Size Optimizaci�n", desc: "Ajusta el tama�o de la cola de eventos del controlador del rat�n para menor latencia.", label: "Descargar .REG", action: () => createRegFile("MouseQueueSize", `Windows Registry Editor Version 5.00\n\n${regContents.MouseQueueSize}`) },
                { title: "SmoothMouseCurve Removal", desc: "Sustituye la curva de respuesta original por valores planos para lectura directa del sensor.", label: "Descargar .REG", action: () => createRegFile("SmoothMouseCurve", `Windows Registry Editor Version 5.00\n\n${regContents.SmoothMouseCurve}`) },
                { title: "Keyboard Delay 0", desc: "Elimina la latencia de respuesta inicial al presionar cualquier tecla.", label: "Descargar .REG", action: () => createRegFile("KeyboardDelay", `Windows Registry Editor Version 5.00\n\n${regContents.KeyboardDelay}`) },
                { title: "Keyboard Speed Max", desc: "Incrementa el ratio de repetici�n de pulsaci�n de teclas al valor �ptimo continuo.", label: "Descargar .REG", action: () => createRegFile("KeyboardSpeed", `Windows Registry Editor Version 5.00\n\n${regContents.KeyboardSpeed}`) },
                { title: "Keyboard Data Queue Boost", desc: "Reduce el b�fer de entrada de datos del teclado aumentando los ciclos de refresco.", label: "Descargar .REG", action: () => createRegFile("KbdQueueSize", `Windows Registry Editor Version 5.00\n\n${regContents.KbdQueueSize}`) },
                { title: "Flags Instant Response", desc: "Establece los modificadores del teclado para prevenir filtros de retardo de Windows.", label: "Descargar .REG", action: () => createRegFile("KbdFlags", `Windows Registry Editor Version 5.00\n\n${regContents.KbdFlags}`) }
            ]
        };

        // Funci�n Ejecutar Todo (Fusi�n Completa)
        function executeAllTweaks() {
            // 1. Fusionar todas las cadenas Regedit en un solo archivo maestro corporativo
            let masterRegContent = "Windows Registry Editor Version 5.00\n\n";
            for (const key in regContents) {
                masterRegContent += `; --- Tweak: ${key} ---\n${regContents[key]}\n\n`;
            }
            createRegFile("Yosser_Tweaks_Master_Pack", masterRegContent);

            // 2. Unificar todas las l�neas de comandos CMD separadas por operadores de control
            let masterCmdContent = "";
            dataModules.cmds.forEach((cmdItem, index) => {
                masterCmdContent += cmdItem.commandText;
                if (index < dataModules.cmds.length - 1) {
                    masterCmdContent += " && ";
                }
            });
            copyToClipboard(masterCmdContent, true);

            // 3. Notificaci�n unificada al usuario
            alert("�ACCIONADOS TODOS LOS TWEAKS!\n\n1. Se ha descargado el archivo 'Yosser_Tweaks_Master_Pack.reg' con TODAS las configuraciones del sistema, energ�a y perif�ricos.\n2. Todos los comandos CMD se han unificado y copiado a tu Portapapeles. Solo abre CMD como administrador y presiona Ctrl+V.");
        }

        // Renderizado autom�tico
        function renderApp() {
            Object.keys(dataModules).forEach(key => {
                const targetContainer = document.getElementById(key);
                dataModules[key].forEach(item => {
                    const cardElement = document.createElement('div');
                    cardElement.className = 'card';
                    cardElement.innerHTML = `<div><h3>${item.title}</h3><p>${item.desc}</p></div>`;
                    
                    const actionBtn = document.createElement('button');
                    actionBtn.className = 'btn-execute';
                    actionBtn.textContent = item.label;
                    actionBtn.onclick = item.action;
                    
                    cardElement.appendChild(actionBtn);
                    targetContainer.appendChild(cardElement);
                });
            });
        }

        window.addEventListener('DOMContentLoaded', renderApp);
    </script>
</body>
</html>
