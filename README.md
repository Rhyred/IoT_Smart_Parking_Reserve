graph TD
    subgraph "Lapisan Pengguna (User Layer)"
        U[<i class="fa fa-user"></i> Pengguna]
        WB([<i class="fa fa-window-maximize"></i> Aplikasi Web Frontend])
        CB[<i class="fa fa-comment-dots"></i> AI Chatbot]
        MOB(<i class="fa fa-mobile-alt"></i> Aplikasi Mobile - Flutter<br/><i>(Rencana)</i>)
    end

    subgraph "Lapisan Layanan Backend (Backend Services)"
        MikhPau[<i class="fa fa-cogs"></i> Modul MikhPau<br/><i>(Monitoring MikroTik)</i>]
        HuaPau[<i class="fa fa-cogs"></i> Modul HuaPau<br/><i>(Monitoring Huawei)</i>]
        DdosApi[<i class="fa fa-shield-alt"></i> DdosApi Service<br/>(Deteksi AI)]
    end

    subgraph "Model AI (Internal)"
        AI_Model[<i class="fa fa-brain"></i> network_monitoring_ai<br/><i>(Autoencoder Model)</i>]
    end

    subgraph "Lapisan Perangkat (Hardware Layer)"
        MikroTik[<i class="fa fa-server"></i> Perangkat MikroTik]
        Huawei[<i class="fa fa-server"></i> Perangkat Huawei]
    end

    %% --- Connections ---
    U --> WB
    WB -- Interaksi --> CB
    WB -- Minta Status & Hasil Deteksi (API Call) --> MikhPau
    WB -- Minta Status & Hasil Deteksi (API Call) --> HuaPau
    WB -- Minta Status & Hasil Deteksi (API Call) --> DdosApi

    MikhPau -- Ambil Data (RouterOS API/SSH) --> MikroTik
    HuaPau -- Ambil Data (SNMP/NETCONF) --> Huawei

    MikhPau -- Kirim Data Trafik --> DdosApi
    HuaPau -- Kirim Data Trafik --> DdosApi
    DdosApi -- Menggunakan --> AI_Model
