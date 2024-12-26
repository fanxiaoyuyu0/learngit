graph TD
    A[Go Client] --> B[WFP]
    B --> C[WM_START_ACC or LSP_WND_START_ACC]
    C --> D[SyncConfig]
    B --> E[WM_STOP_ACC or LSP_WND_STOP_ACC]
    E --> D
    B --> F[WM_QUIT_ACC]
    F --> G[stopAcc and QuitMessage]
    
    B --> H[timer]
    H --> I[WM_TIMER wParam is TIMER_CHECK_TRAYSTATE]
    I --> J[Don't found hTrayWindow]
    J --> K[stopAcc and QuitMessage]
    I --> L[New hTrayWindow]
    L --> D

    B --> M[wfp -> Go Client]
    M --> N[WM_CREATE]
    N --> O[copy & move 驱动文件]
    N --> P[nf_registerDriver 注册驱动]
    N --> Q[通知gHeyboxTrayWindow 驱动注册结果]
    Q --> R[记录未使用结果]
    
    M --> S[StartAcc]
    S --> T[wfp -> Go Client 发送 SYSTRAY_CONNECT_WFP_RESULT消息]
    S --> U[清空filter rules]
    S --> V[更新filter rules]

    M --> W[StopAcc]
    W --> U[清空filter rules]
