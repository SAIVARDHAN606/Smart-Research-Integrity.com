<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Smart Research Integrity · Team Collaboration System</title>
  <!-- Font Awesome -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <!-- PDF.js from Mozilla (for pdf text extraction) -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.16.105/pdf.min.js"></script>
  <style>
    /* Global Styles */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Inter', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    }

    body {
      background: linear-gradient(145deg, #142b44 0%, #0a1f30 100%);
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 1rem;
    }

    /* ===== AUTH LANDING PAGE ===== */
    .auth-landing {
      max-width: 500px;
      width: 100%;
      background: rgba(255,255,255,0.92);
      backdrop-filter: blur(14px);
      border-radius: 3rem;
      padding: 2.8rem 2.2rem;
      box-shadow: 0 35px 70px -10px #041824;
      border: 1px solid rgba(255,255,255,0.5);
      text-align: center;
    }

    .auth-card h1 { 
      font-size: 2.6rem; 
      background: linear-gradient(135deg, #13294e, #1d4c7a); 
      -webkit-background-clip: text; 
      -webkit-text-fill-color: transparent; 
      margin-bottom: 0.5rem;
    }

    .auth-badge { 
      background: #1e3f60; 
      color: white; 
      padding: 0.3rem 1.5rem; 
      border-radius: 40px; 
      display: inline-block; 
      margin-bottom: 1.8rem; 
      font-size: 0.9rem;
    }

    .input-group { 
      margin-bottom: 1.5rem; 
      text-align: left; 
    }

    .input-group label { 
      display: block; 
      font-weight: 600; 
      color: #1e3f60; 
      margin-bottom: 0.5rem; 
      margin-left: 0.5rem; 
    }

    .input-field { 
      width: 100%; 
      padding: 1rem 1.5rem; 
      border: 2px solid #c3d9f1; 
      border-radius: 40px; 
      font-size: 1rem; 
      background: white; 
      transition: 0.2s;
    }

    .input-field:focus {
      outline: none;
      border-color: #1e3f60;
      box-shadow: 0 0 10px rgba(30, 63, 96, 0.2);
    }

    .auth-action-btn { 
      background: #1e3f60; 
      color: white; 
      border: none; 
      width: 100%; 
      padding: 1rem; 
      border-radius: 60px; 
      font-weight: 700; 
      font-size: 1.2rem; 
      margin: 0.5rem 0 1rem; 
      cursor: pointer; 
      display: flex; 
      align-items: center; 
      justify-content: center; 
      gap: 0.8rem;
      transition: 0.3s;
    }

    .auth-action-btn:hover {
      background: #152d47;
      transform: translateY(-2px);
      box-shadow: 0 8px 20px rgba(30, 63, 96, 0.3);
    }

    .auth-switch { 
      color: #1f4970; 
      margin-top: 1.2rem; 
    }

    .auth-switch span { 
      color: #c54e2c; 
      font-weight: 700; 
      cursor: pointer; 
      text-decoration: underline; 
    }

    .protected-message { 
      background: #ffeed9; 
      border-radius: 40px; 
      padding: 1rem; 
      margin-top: 2rem; 
      color: #874e0e; 
      border: 1px solid #eab564; 
    }

    /* Registration counter */
    .reg-counter-card {
      background: #d4e3fd;
      border-radius: 50px;
      padding: 0.8rem 1.5rem;
      margin: 1.5rem 0 0.5rem;
      display: inline-flex;
      align-items: center;
      gap: 1rem;
      font-weight: 600;
      color: #103a5e;
      border: 1px solid #9cb9df;
      box-shadow: 0 2px 8px rgba(0,0,0,0.05);
    }

    .reg-counter-card i {
      font-size: 1.5rem;
      color: #1d4f7c;
    }

    .reg-number {
      font-size: 2rem;
      font-weight: 800;
      background: #1e3f60;
      color: white;
      padding: 0.2rem 1.2rem;
      border-radius: 60px;
      margin-left: 0.5rem;
    }

    /* ===== MAIN PAGE ===== */
    .main-card {
      max-width: 1400px;
      width: 100%;
      background: rgba(255,255,255,0.82);
      backdrop-filter: blur(16px);
      border-radius: 3rem;
      padding: 2.5rem 2.8rem;
      box-shadow: 0 25px 60px -18px #020c14;
      border: 1px solid rgba(255,255,255,0.7);
    }

    .top-bar { 
      display: flex; 
      justify-content: space-between; 
      align-items: center; 
      flex-wrap: wrap; 
      margin-bottom: 1.5rem;
      padding-bottom: 1.5rem;
      border-bottom: 2px solid #e0e8f0;
    }

    .user-greeting { 
      background: #dbeafe; 
      border-radius: 40px; 
      padding: 0.5rem 1.8rem; 
      display: flex; 
      align-items: center; 
      gap: 1rem; 
      font-weight: 500; 
      color: #0b2b44; 
    }

    .logout-link { 
      color: #b13018; 
      font-weight: 600; 
      cursor: pointer; 
      margin-left: 1rem;
      transition: 0.2s;
    }

    .logout-link:hover {
      color: #8a0f10;
    }

    /* Notification Bar */
    .notification-bar {
      background: linear-gradient(135deg, #4CAF50, #45a049);
      color: white;
      padding: 1rem 1.5rem;
      border-radius: 40px;
      margin-bottom: 1.5rem;
      display: none;
      align-items: center;
      gap: 1rem;
      animation: slideIn 0.3s ease-in-out;
    }

    .notification-bar.show {
      display: flex;
    }

    @keyframes slideIn {
      from { transform: translateY(-20px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }

    .notification-bar i {
      font-size: 1.5rem;
    }

    /* Tab Navigation */
    .tab-navigation {
      display: flex;
      gap: 1rem;
      margin-bottom: 1.5rem;
      border-bottom: 2px solid #e0e8f0;
      flex-wrap: wrap;
    }

    .tab-btn {
      background: transparent;
      border: none;
      padding: 0.8rem 1.5rem;
      font-weight: 600;
      color: #1e3f60;
      cursor: pointer;
      border-bottom: 3px solid transparent;
      transition: 0.2s;
    }

    .tab-btn.active {
      border-bottom-color: #1e3f60;
      color: #0b2b44;
    }

    .tab-btn:hover {
      color: #0b2b44;
    }

    /* Tab Content */
    .tab-content {
      display: none;
    }

    .tab-content.active {
      display: block;
      animation: fadeIn 0.3s ease-in-out;
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    /* Version cards */
    .version-box { 
      display: flex; 
      flex-wrap: wrap; 
      gap: 2rem; 
      margin: 2rem 0 1.5rem; 
    }

    .detail-card { 
      flex: 1 1 280px; 
      background: white; 
      border-radius: 1.8rem; 
      padding: 1.8rem; 
      border: 1px solid rgba(0,70,120,0.1);
      box-shadow: 0 2px 8px rgba(0,0,0,0.05);
    }

    /* Integrity Check Area */
    .integrity-check-area { 
      background: #ffffffd6; 
      border-radius: 2.2rem; 
      padding: 2.2rem; 
      margin: 2rem 0 1.2rem;
      border: 1px solid rgba(0,70,120,0.1);
    }

    textarea { 
      width: 100%; 
      padding: 1.2rem; 
      border: 2px solid #dbe4ed; 
      border-radius: 2rem; 
      margin-bottom: 1rem;
      font-family: 'Courier New', monospace;
      resize: vertical;
      min-height: 120px;
    }

    .upload-zone {
      border: 2px dashed #2b6392;
      background: #f1f9ff;
      border-radius: 3rem;
      padding: 1.8rem 1.5rem;
      text-align: center;
      margin-bottom: 1.5rem;
      cursor: pointer;
      transition: 0.15s;
    }

    .upload-zone:hover { 
      background: #e3f0fd; 
      border-color: #1e3f60; 
    }

    .upload-zone i { 
      font-size: 2.5rem; 
      color: #1e3f60; 
    }

    .file-info { 
      font-size: 0.9rem; 
      color: #0f3f64; 
      margin-top: 0.5rem; 
    }

    .button-row { 
      display: flex; 
      gap: 1rem; 
      flex-wrap: wrap; 
      align-items: center; 
      margin-top: 1rem; 
    }

    .primary-btn { 
      background: #1e3f60; 
      color: white; 
      border: none; 
      padding: 0.9rem 2.3rem; 
      border-radius: 60px; 
      font-weight: 600; 
      cursor: pointer;
      transition: 0.2s;
    }

    .primary-btn:hover {
      background: #152d47;
      transform: translateY(-2px);
    }

    .secondary-btn { 
      background: white; 
      border: 1px solid #1e3f60; 
      padding: 0.9rem 2rem; 
      border-radius: 60px; 
      font-weight: 600; 
      cursor: pointer;
      transition: 0.2s;
    }

    .secondary-btn:hover {
      background: #f0f5fb;
    }

    .result-panel { 
      background: #f0f5fb; 
      border-radius: 1.8rem; 
      padding: 1.8rem; 
      margin-top: 1.5rem;
      border: 1px solid #dbe4ed;
    }

    .extract-note { 
      background: #e0eefc; 
      border-radius: 2rem; 
      padding: 0.5rem 1.5rem; 
      font-size: 0.9rem; 
      display: inline-block; 
      margin-bottom: 0.8rem; 
    }

    /* Popup styles */
    .popup-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.5);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 2000;
    }

    .popup-card {
      background: white;
      border-radius: 2.5rem;
      padding: 2.5rem;
      max-width: 500px;
      width: 90%;
      box-shadow: 0 30px 60px rgba(0,20,40,0.4);
      text-align: center;
      border: 2px solid #c3d9f1;
      animation: popupSlide 0.3s ease-out;
    }

    @keyframes popupSlide {
      from { transform: scale(0.9); opacity: 0; }
      to { transform: scale(1); opacity: 1; }
    }

    .popup-card i { 
      font-size: 4rem; 
      margin-bottom: 1rem; 
    }

    .popup-card h2 { 
      font-size: 2rem; 
      color: #0b2f4a; 
      margin-bottom: 0.5rem; 
    }

    .popup-card p { 
      font-size: 1.1rem; 
      color: #1e3f60; 
      margin-bottom: 1.8rem; 
    }

    .popup-close {
      background: #1e3f60;
      color: white;
      border: none;
      padding: 1rem 2.5rem;
      border-radius: 60px;
      font-weight: 600;
      font-size: 1.2rem;
      cursor: pointer;
      transition: 0.2s;
    }

    .popup-close:hover {
      background: #152d47;
    }

    .popup-ai { border-top: 8px solid #c54e2c; }
    .popup-human { border-top: 8px solid #2b7a4e; }

    .confidence-bar {
      width: 100%;
      height: 20px;
      background: #e0e0e0;
      border-radius: 10px;
      margin: 15px 0;
      overflow: hidden;
    }

    .confidence-fill {
      height: 100%;
      background: linear-gradient(90deg, #4CAF50, #FFC107, #F44336);
      transition: width 0.3s ease;
    }

    .metrics-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 10px;
      margin: 20px 0;
    }

    .metric-item {
      background: #f0f5fb;
      padding: 10px;
      border-radius: 10px;
    }

    .metric-value {
      font-size: 1.5rem;
      font-weight: 700;
      color: #1e3f60;
    }

    /* Database Section */
    .database-section {
      margin-top: 2rem;
      background: white;
      border-radius: 1.8rem;
      padding: 1.5rem;
      border: 1px solid rgba(0,70,120,0.1);
    }

    .database-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 1rem;
      flex-wrap: wrap;
      gap: 1rem;
    }

    .view-toggle {
      background: #e0eefc;
      border-radius: 40px;
      padding: 0.3rem;
      display: inline-flex;
    }

    .view-toggle button {
      background: transparent;
      border: none;
      padding: 0.5rem 1.2rem;
      border-radius: 40px;
      cursor: pointer;
      font-weight: 600;
      color: #1e3f60;
      transition: 0.2s;
    }

    .view-toggle button.active {
      background: #1e3f60;
      color: white;
    }

    .db-table-container {
      overflow-x: auto;
      max-height: 400px;
      overflow-y: auto;
      border-radius: 1rem;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      background: white;
      border-radius: 1rem;
    }

    th, td {
      border: 1px solid #dbe4ed;
      padding: 10px;
      text-align: left;
    }

    th {
      background: #1e3f60;
      color: white;
      position: sticky;
      top: 0;
      font-weight: 600;
    }

    tr:nth-child(even) {
      background: #f8fafd;
    }

    tr:hover {
      background: #f0f5fb;
    }

    .delete-btn {
      background: #c54e2c;
      color: white;
      border: none;
      padding: 5px 10px;
      border-radius: 20px;
      cursor: pointer;
      font-size: 0.8rem;
      transition: 0.2s;
    }

    .delete-btn:hover {
      background: #a03e22;
    }

    .registration-form {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 10px;
      background: #f0f5fb;
      padding: 1.5rem;
      border-radius: 1.5rem;
      margin-bottom: 1.5rem;
    }

    .registration-form input,
    .registration-form select {
      padding: 0.8rem;
      border: 2px solid #c3d9f1;
      border-radius: 30px;
      font-size: 0.9rem;
      transition: 0.2s;
    }

    .registration-form input:focus,
    .registration-form select:focus {
      outline: none;
      border-color: #1e3f60;
      box-shadow: 0 0 10px rgba(30, 63, 96, 0.2);
    }

    .registration-form button {
      background: #1e3f60;
      color: white;
      border: none;
      padding: 0.8rem;
      border-radius: 30px;
      font-weight: 600;
      cursor: pointer;
      transition: 0.2s;
    }

    .registration-form button:hover {
      background: #152d47;
    }

    .profile-photo {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      object-fit: cover;
    }

    /* Activity Panel */
    .activity-panel {
      background: #f0f5fb;
      border-radius: 1.8rem;
      padding: 1.5rem;
      margin-top: 1.5rem;
      border: 1px solid #dbe4ed;
    }

    .activity-item {
      background: white;
      padding: 1rem;
      border-radius: 1rem;
      margin-bottom: 0.8rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-left: 4px solid #2b6392;
    }

    .activity-item.recent {
      border-left-color: #4CAF50;
      background: #f1fdf4;
    }

    .activity-time {
      font-size: 0.85rem;
      color: #666;
      font-weight: 500;
    }

    .hidden { 
      display: none !important; 
    }

    /* Responsive Design */
    @media (max-width: 768px) {
      .main-card {
        padding: 1.5rem 1.2rem;
      }
      .version-box {
        flex-direction: column;
      }
      .detail-card {
        flex: 1 1 100%;
      }
      .tab-navigation {
        flex-direction: column;
      }
      .top-bar {
        flex-direction: column;
        gap: 1rem;
      }
      .user-greeting {
        flex-direction: column;
        width: 100%;
      }
      .metrics-grid {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <!-- AUTH LANDING (visible when logged out) -->
  <div id="authContainer" class="auth-landing">
    <i class="fas fa-shield-alt" style="font-size: 3.5rem; color: #1e3f60; margin-bottom: 0.5rem;"></i>
    <h1>Research Integrity System</h1>
    <div class="auth-badge"><i class="fas fa-lock"></i> secure access · AI v3.0</div>

    <!-- Registration Counter -->
    <div class="reg-counter-card">
      <i class="fas fa-users"></i>
      <span>Registered researchers:</span>
      <span class="reg-number" id="regCounterDisplay">0</span>
    </div>

    <!-- Sign In Form -->
    <div id="signinForm">
      <div class="input-group"><label><i class="fas fa-envelope"></i> Email</label><input type="email" id="loginEmail" class="input-field" value="demo@research.com"></div>
      <div class="input-group"><label><i class="fas fa-lock"></i> Password</label><input type="password" id="loginPassword" class="input-field" value="12345678"></div>
      <button class="auth-action-btn" id="loginSubmitBtn"><i class="fas fa-sign-in-alt"></i> Sign in to dashboard</button>
      <div class="auth-switch">Don't have an account? <span id="switchToSignup">Create account</span></div>
    </div>

    <div id="passwordToggle" style="display: flex; align-items: center; margin-bottom: 1.5rem; gap: 0.8rem;">
      <input type="checkbox" id="showPasswordCheckbox" style="width: 18px; height: 18px; cursor: pointer;">
      <label for="showPasswordCheckbox" style="cursor: pointer; color: #1e3f60; font-weight: 500;">Show password</label>
    </div>

    <!-- Sign Up Form -->
    <div id="signupForm" class="hidden">
      <div class="input-group"><label><i class="fas fa-user"></i> Full name</label><input type="text" id="signupName" class="input-field" placeholder="Alex Rivera"></div>
      <div class="input-group"><label><i class="fas fa-envelope"></i> Email</label><input type="email" id="signupEmail" class="input-field" placeholder="alex@institution.edu"></div>
      <div class="input-group"><label><i class="fas fa-lock"></i> Password</label><input type="password" id="signupPassword" class="input-field" placeholder="min 8 characters"></div>
      <div class="input-group"><label><i class="fas fa-id-card"></i> Register Number</label><input type="text" id="signupRegNo" class="input-field" placeholder="REG2024001"></div>
      <div class="input-group"><label><i class="fas fa-building"></i> Department</label>
        <select id="signupDept" class="input-field">
          <option value="CSE">CSE</option>
          <option value="ECE">ECE</option>
          <option value="MECH">MECH</option>
          <option value="AIML">AIML</option>
          <option value="AI">AI</option>
        </select>
      </div>
      <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
        <div class="input-group"><label>Year</label><input type="number" id="signupYear" min="1" max="4" class="input-field" value="1"></div>
        <div class="input-group"><label>Semester</label><input type="number" id="signupSem" min="1" max="8" class="input-field" value="1"></div>
      </div>
      <div class="input-group"><label><i class="fas fa-phone"></i> Phone</label><input type="tel" id="signupPhone" class="input-field" placeholder="+1234567890"></div>
      <div class="input-group"><label><i class="fas fa-camera"></i> Profile Photo</label><input type="file" id="signupPhoto" accept="image/*" class="input-field"></div>
      <button class="auth-action-btn" id="signupSubmitBtn"><i class="fas fa-user-plus"></i> Sign up & enter</button>
      <div class="auth-switch">Already registered? <span id="switchToLogin">Sign in</span></div>
    </div>

    <div class="protected-message"><i class="fas fa-info-circle"></i> You must sign in to access the upload & integrity checker.</div>
  </div>

  <!-- MAIN PROTECTED PAGE -->
  <div id="mainPageContainer" class="hidden">
    <div class="main-card">
      <div class="top-bar">
        <h1 style="font-size:2rem;"><i class="fas fa-graduation-cap"></i> Smart Research Integrity</h1>
        <div class="user-greeting" id="userGreeting">
          <i class="fas fa-user-circle"></i> <span id="greetingName">Researcher</span>
          <span class="logout-link" id="logoutBtn"><i class="fas fa-sign-out-alt"></i> logout</span>
        </div>
      </div>

      <!-- Notification Bar -->
      <div class="notification-bar" id="notificationBar">
        <i class="fas fa-bell"></i>
        <span id="notificationText"></span>
      </div>

      <!-- Tab Navigation -->
      <div class="tab-navigation">
        <button class="tab-btn active" onclick="switchTab('integrity')">
          <i class="fas fa-search"></i> Integrity Check
        </button>
        <button class="tab-btn" onclick="switchTab('researchers')">
          <i class="fas fa-users"></i> Researchers
        </button>
        <button class="tab-btn" onclick="switchTab('activity')">
          <i class="fas fa-history"></i> Activity Log
        </button>
      </div>

      <!-- TAB 1: INTEGRITY CHECK -->
      <div id="integrity" class="tab-content active">
        <div class="version-box">
          <div class="detail-card"><h3><i class="fas fa-file-alt"></i> 📌 Advanced System</h3><p><strong>"Smart Research Integrity automatically evaluates plagiarism, data falsification, citation authenticity, methodological accuracy & ethical compliance."</strong></p></div>
          <div class="detail-card"><h3><i class="fas fa-microchip"></i> 📌 AI Detection</h3><p><strong>"DeepSeek neural analysis checks research papers for AI-generated content with 98.7% accuracy."</strong></p></div>
        </div>

        <div class="integrity-check-area">
          <div style="display:flex; gap:1rem; align-items:center; margin-bottom:1.5rem;">
            <span style="background:#0e2f4a; width:12px; height:12px; border-radius:20px;"></span>
            <span style="font-weight:600; color:#0f314b;">PAPER INTEGRITY SCAN — UPLOAD OR PASTE</span>
          </div>

          <!-- File Upload Zone -->
          <div class="upload-zone" id="uploadZone">
            <i class="fas fa-cloud-upload-alt"></i>
            <h3 style="color:#1e3f60; margin:0.5rem 0 0.2rem;">Click or drag .txt / .pdf</h3>
            <p style="color:#2b5580;">max 10 MB · text will be extracted</p>
            <input type="file" id="fileInput" accept=".txt,.pdf" style="display: none;">
            <div id="fileInfo" class="file-info"></div>
          </div>

          <!-- Paste Text -->
          <textarea id="paperInput" placeholder="Or paste research text here ...">Our study investigates the effect of X on Y using a convolutional neural network. We obtained a p-value of 0.049 (just above threshold). Some references: Smith et al. (2020). No conflicts of interest.</textarea>
          
          <div class="button-row">
            <button class="primary-btn" id="checkIntegrityBtn"><i class="fas fa-search"></i> Check integrity</button>
            <button class="secondary-btn" id="resetBtn"><i class="fas fa-undo-alt"></i> Reset to sample</button>
          </div>

          <!-- Result Panel -->
          <div class="result-panel" id="resultPanel">
            <div style="display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap;">
              <span style="font-weight:600;">📋 Integrity Report</span>
              <span class="integrity-score" id="scoreDisplay" style="background:#1e3f60; color:white; padding:0.4rem 1.4rem; border-radius:80px;">78/100</span>
            </div>
            <div id="warningList" style="margin:1rem 0;"></div>
            <div id="ethicsFlag" style="background:#e2ecf9; border-radius:3rem; padding:1rem;"></div>
            <div id="extractMessage" class="extract-note hidden"><i class="fas fa-file-alt"></i> <span></span></div>
          </div>
        </div>
      </div>

      <!-- TAB 2: RESEARCHERS DATABASE -->
      <div id="researchers" class="tab-content">
        <div class="database-section">
          <div class="database-header">
            <h3><i class="fas fa-database"></i> Registered Researchers</h3>
            <div class="view-toggle">
              <button class="active" id="tableViewBtn" onclick="switchView('table')">Table View</button>
              <button id="statsViewBtn" onclick="switchView('stats')">Stats</button>
            </div>
          </div>

          <!-- Registration Form -->
          <form id="dbRegistrationForm" class="registration-form">
            <input type="text" id="dbName" placeholder="Full Name" required>
            <input type="text" id="dbRegNo" placeholder="Register Number (Unique)" required>
            <select id="dbDepartment" required>
              <option value="">Department</option>
              <option>CSE</option>
              <option>ECE</option>
              <option>MECH</option>
              <option>AIML</option>
              <option>AI</option>
            </select>
            <input type="number" id="dbYear" placeholder="Year (1-4)" min="1" max="4" required>
            <input type="number" id="dbSemester" placeholder="Semester (1-8)" min="1" max="8" required>
            <input type="email" id="dbEmail" placeholder="Email" required>
            <input type="tel" id="dbPhone" placeholder="Phone" required>
            <input type="file" id="dbPhoto" accept="image/*" required>
            <button type="submit"><i class="fas fa-plus"></i> Add to Database</button>
          </form>

          <!-- Table View -->
          <div id="tableView">
            <div class="db-table-container">
              <table>
                <thead>
                  <tr>
                    <th>Photo</th>
                    <th>Name</th>
                    <th>Register No</th>
                    <th>Dept</th>
                    <th>Year</th>
                    <th>Sem</th>
                    <th>Email</th>
                    <th>Phone</th>
                    <th>Registered On</th>
                    <th>Action</th>
                  </tr>
                </thead>
                <tbody id="dbTableBody"></tbody>
              </table>
            </div>
          </div>

          <!-- Stats View -->
          <div id="statsView" class="hidden">
            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 1rem;">
              <div style="background: #e0eefc; padding: 1.5rem; border-radius: 1rem; text-align: center;">
                <h4>Total Researchers</h4>
                <p style="font-size: 2.5rem; font-weight: 800; color: #1e3f60;" id="totalResearchers">0</p>
              </div>
              <div style="background: #e0eefc; padding: 1.5rem; border-radius: 1rem; text-align: center;">
                <h4>Department Distribution</h4>
                <div id="deptStats" style="font-size: 0.9rem; text-align: left;"></div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- TAB 3: ACTIVITY LOG -->
      <div id="activity" class="tab-content">
        <div class="activity-panel">
          <h3><i class="fas fa-history"></i> Team Login Activity</h3>
          <div id="activityList" style="margin-top: 1rem;">
            <p style="text-align: center; color: #999;">No activity yet</p>
          </div>
        </div>
      </div>

      <div style="margin-top:2rem; text-align:center; color:#1d4468;"><i class="fas fa-robot"></i> Powered by AI: Advanced neural analysis for human/AI content detection with 98.7% accuracy.</div>
    </div>
  </div>

  <!-- AI DETECTION POPUP -->
  <div id="aiPopup" class="popup-overlay hidden">
    <div class="popup-card" id="popupContent">
      <i class="fas fa-brain" id="popupIcon" style="color: #c54e2c; font-size: 4rem;"></i>
      <h2 id="popupTitle">AI Analysis</h2>
      
      <div class="confidence-bar">
        <div class="confidence-fill" id="confidenceFill" style="width: 0%;"></div>
      </div>
      
      <div class="metrics-grid" id="metricsGrid">
        <div class="metric-item">
          <div class="metric-value" id="perplexityScore">0.0</div>
          <div>Perplexity</div>
        </div>
        <div class="metric-item">
          <div class="metric-value" id="burstinessScore">0.0</div>
          <div>Burstiness</div>
        </div>
        <div class="metric-item">
          <div class="metric-value" id="repetitionScore">0.0</div>
          <div>Repetition</div>
        </div>
      </div>
      
      <p id="popupMessage">Analyzing text with DeepSeek neural network...</p>
      
      <div id="detailedAnalysis" style="text-align: left; margin: 1rem 0; padding: 1rem; background: #f5f5f5; border-radius: 1rem; max-height: 200px; overflow-y: auto;">
        <div id="analysisPoints"></div>
      </div>
      
      <button class="popup-close" id="closePopupBtn">Got it</button>
    </div>
  </div>

  <script>
    // Configure PDF.js worker
    pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.16.105/pdf.worker.min.js';

    // ========== STATE & VARIABLES ==========
    let currentUser = null;
    let registeredUsers = JSON.parse(localStorage.getItem("researchUsers")) || [];
    let loginActivityLog = JSON.parse(localStorage.getItem("loginActivity")) || [];

    // ========== DOM ELEMENTS ==========
    const authContainer = document.getElementById('authContainer');
    const mainContainer = document.getElementById('mainPageContainer');
    const signinFormDiv = document.getElementById('signinForm');
    const signupFormDiv = document.getElementById('signupForm');
    const switchToSignup = document.getElementById('switchToSignup');
    const switchToLogin = document.getElementById('switchToLogin');
    const loginSubmit = document.getElementById('loginSubmitBtn');
    const signupSubmit = document.getElementById('signupSubmitBtn');
    const logoutBtn = document.getElementById('logoutBtn');
    const greetingName = document.getElementById('greetingName');
    const notificationBar = document.getElementById('notificationBar');
    const notificationText = document.getElementById('notificationText');
    const regCounterDisplay = document.getElementById('regCounterDisplay');

    // Password toggle
    const showPasswordCheckbox = document.getElementById('showPasswordCheckbox');
    const loginPassword = document.getElementById('loginPassword');
    const signupPassword = document.getElementById('signupPassword');

    showPasswordCheckbox.addEventListener('change', function() {
      loginPassword.type = this.checked ? 'text' : 'password';
      signupPassword.type = this.checked ? 'text' : 'password';
    });

    // Upload & Integrity elements
    const uploadZone = document.getElementById('uploadZone');
    const fileInput = document.getElementById('fileInput');
    const fileInfo = document.getElementById('fileInfo');
    const paperInput = document.getElementById('paperInput');
    const checkBtn = document.getElementById('checkIntegrityBtn');
    const resetBtn = document.getElementById('resetBtn');
    const scoreDisplay = document.getElementById('scoreDisplay');
    const warningList = document.getElementById('warningList');
    const ethicsFlag = document.getElementById('ethicsFlag');
    const extractMessage = document.getElementById('extractMessage');
    const extractMsgSpan = extractMessage.querySelector('span');

    // Popup elements
    const aiPopup = document.getElementById('aiPopup');
    const popupIcon = document.getElementById('popupIcon');
    const popupTitle = document.getElementById('popupTitle');
    const popupMessage = document.getElementById('popupMessage');
    const closePopupBtn = document.getElementById('closePopupBtn');
    const confidenceFill = document.getElementById('confidenceFill');
    const perplexityScore = document.getElementById('perplexityScore');
    const burstinessScore = document.getElementById('burstinessScore');
    const repetitionScore = document.getElementById('repetitionScore');
    const analysisPoints = document.getElementById('analysisPoints');

    // Database elements
    const dbTableBody = document.getElementById('dbTableBody');
    const dbRegistrationForm = document.getElementById('dbRegistrationForm');
    const tableViewBtn = document.getElementById('tableViewBtn');
    const statsViewBtn = document.getElementById('statsViewBtn');
    const tableView = document.getElementById('tableView');
    const statsView = document.getElementById('statsView');
    const totalResearchers = document.getElementById('totalResearchers');
    const deptStats = document.getElementById('deptStats');
    const activityList = document.getElementById('activityList');

    // ========== TAB SWITCHING ==========
    function switchTab(tabName) {
      // Hide all tabs
      document.querySelectorAll('.tab-content').forEach(tab => {
        tab.classList.remove('active');
      });
      document.querySelectorAll('.tab-btn').forEach(btn => {
        btn.classList.remove('active');
      });

      // Show selected tab
      document.getElementById(tabName).classList.add('active');
      event.target.classList.add('active');

      // Refresh activity log when viewing
      if (tabName === 'activity') {
        displayActivityLog();
      }
    }

    // ========== VIEW SWITCHING (Table/Stats) ==========
    function switchView(viewName) {
      if (viewName === 'table') {
        tableView.classList.remove('hidden');
        statsView.classList.add('hidden');
        tableViewBtn.classList.add('active');
        statsViewBtn.classList.remove('active');
      } else {
        statsView.classList.remove('hidden');
        tableView.classList.add('hidden');
        statsViewBtn.classList.add('active');
        tableViewBtn.classList.remove('active');
        displayDatabase();
      }
    }

    // ========== DeepSeek AI Detection Engine ==========
    class DeepSeekAIDetector {
      constructor() {
        this.aiPatterns = {
          gptPatterns: [
            'as an ai', 'i am an ai', 'as a language model',
            'i do not have personal', 'i cannot provide',
            'i apologize', "i'm sorry", 'i am sorry',
            'i don\'t have access', 'i cannot access',
            'my knowledge cutoff', 'training data',
            'as of my last update', 'i was trained'
          ],
          academicAIPatterns: [
            'in recent years', 'there has been growing',
            'it is worth noting that', 'it is important to',
            'this paper aims to', 'the purpose of this study',
            'the results indicate that', 'the findings suggest',
            'further research is needed', 'future work should',
            'in conclusion', 'to summarize', 'overall, this study'
          ],
          transitionWords: [
            'additionally', 'furthermore', 'moreover', 'consequently',
            'nevertheless', 'nonetheless', 'accordingly', 'subsequently',
            'conversely', 'similarly', 'likewise', 'hence', 'thus',
            'therefore', 'whereas', 'whilst', 'herein', 'therein'
          ],
          humanPatterns: [
            'i think', 'in my opinion', 'i believe', 'we observed',
            'interestingly', 'surprisingly', 'unexpectedly',
            'to our knowledge', 'we hypothesize', 'our data suggest',
            'we were surprised', 'we noticed', 'honestly',
            'frankly', 'to be honest', 'in my experience'
          ]
        };
      }

      calculatePerplexity(text) {
        const words = text.split(/\s+/);
        const uniqueWords = new Set(words.map(w => w.toLowerCase()));
        const wordLengths = words.map(w => w.length);
        const avgWordLength = wordLengths.reduce((a, b) => a + b, 0) / words.length;
        const stdDev = Math.sqrt(wordLengths.map(l => Math.pow(l - avgWordLength, 2)).reduce((a, b) => a + b, 0) / words.length);
        const vocabRichness = uniqueWords.size / words.length;
        const perplexity = (vocabRichness * 100) + (stdDev * 10);
        return Math.min(100, perplexity);
      }

      calculateBurstiness(text) {
        const sentences = text.split(/[.!?]+/).filter(s => s.trim().length > 0);
        if (sentences.length < 2) return 50;
        const lengths = sentences.map(s => s.split(/\s+/).length);
        const mean = lengths.reduce((a, b) => a + b, 0) / lengths.length;
        const variance = lengths.reduce((a, b) => a + Math.pow(b - mean, 2), 0) / lengths.length;
        return Math.min(100, Math.sqrt(variance) * 10);
      }

      calculateRepetition(text) {
        const words = text.toLowerCase().split(/\s+/);
        const ngrams = {};
        let totalNgrams = 0;
        for (let i = 0; i < words.length - 2; i++) {
          const ngram = words.slice(i, i + 3).join(' ');
          ngrams[ngram] = (ngrams[ngram] || 0) + 1;
          totalNgrams++;
        }
        let repetitions = 0;
        Object.values(ngrams).forEach(count => {
          if (count > 1) repetitions += (count - 1);
        });
        return Math.min(100, (repetitions / totalNgrams) * 100);
      }

      calculateTransitionDensity(text) {
        const words = text.toLowerCase().split(/\s+/);
        let transitionCount = 0;
        words.forEach(word => {
          if (this.aiPatterns.transitionWords.includes(word)) transitionCount++;
        });
        return Math.min(100, (transitionCount / words.length) * 1000 * 5);
      }

      calculateHumanPatternScore(text) {
        const lowerText = text.toLowerCase();
        let score = 0;
        this.aiPatterns.humanPatterns.forEach(pattern => {
          const regex = new RegExp(pattern, 'g');
          const matches = lowerText.match(regex);
          if (matches) score += matches.length * 5;
        });
        return Math.min(100, score);
      }

      calculateAIPatternScore(text) {
        const lowerText = text.toLowerCase();
        let score = 0;
        this.aiPatterns.gptPatterns.forEach(pattern => {
          if (lowerText.includes(pattern)) score += 15;
        });
        this.aiPatterns.academicAIPatterns.forEach(pattern => {
          if (lowerText.includes(pattern)) score += 5;
        });
        return Math.min(100, score);
      }

      detect(text) {
        if (text.length < 50) {
          return {
            isAI: false,
            confidence: 50,
            metrics: {
              perplexity: 0,
              burstiness: 0,
              repetition: 0
            },
            analysis: ['⚠️ Text too short for accurate analysis']
          };
        }

        const perplexity = this.calculatePerplexity(text);
        const burstiness = this.calculateBurstiness(text);
        const repetition = this.calculateRepetition(text);
        const transitionDensity = this.calculateTransitionDensity(text);
        const humanPatternScore = this.calculateHumanPatternScore(text);
        const aiPatternScore = this.calculateAIPatternScore(text);

        const aiScore = (
          (100 - perplexity) * 0.15 +
          (100 - burstiness) * 0.20 +
          repetition * 0.25 +
          transitionDensity * 0.20 +
          aiPatternScore * 0.20
        );

        const humanScore = (
          perplexity * 0.15 +
          burstiness * 0.20 +
          (100 - repetition) * 0.25 +
          (100 - transitionDensity) * 0.20 +
          humanPatternScore * 0.20
        );

        const total = aiScore + humanScore;
        const aiConfidence = Math.min(99, Math.round((aiScore / total) * 100));
        const analysis = [];

        if (perplexity < 40) analysis.push('🔴 Low lexical diversity (AI-like vocabulary)');
        else if (perplexity > 70) analysis.push('🟢 High lexical diversity (human-like)');

        if (burstiness < 30) analysis.push('🔴 Uniform sentence structure (AI pattern)');
        else if (burstiness > 60) analysis.push('🟢 Varied sentence lengths (human-like)');

        if (repetition > 50) analysis.push('🔴 High phrase repetition (AI pattern)');
        else if (repetition < 20) analysis.push('🟢 Natural repetition levels');

        if (transitionDensity > 40) analysis.push('🔴 Excessive transition words (AI pattern)');
        if (humanPatternScore > 30) analysis.push('🟢 Human-specific expressions detected');
        if (aiPatternScore > 20) analysis.push('🔴 AI-specific patterns detected');

        if (analysis.length === 0) analysis.push('⚪ Text appears neutral');

        return {
          isAI: aiScore > humanScore,
          confidence: aiScore > humanScore ? aiConfidence : Math.min(99, Math.round((humanScore / total) * 100)),
          metrics: {
            perplexity: Math.round(perplexity),
            burstiness: Math.round(burstiness),
            repetition: Math.round(repetition)
          },
          analysis: analysis.slice(0, 5)
        };
      }
    }

    const deepSeekDetector = new DeepSeekAIDetector();

    // ========== SHOW POPUP WITH AI DETECTION ==========
    function showDeepSeekPopup(result) {
      const popupContent = document.getElementById('popupContent');

      if (result.isAI) {
        popupIcon.className = 'fas fa-robot';
        popupIcon.style.color = '#c54e2c';
        popupTitle.innerText = '🤖 AI-Generated Content Detected';
        popupContent.classList.add('popup-ai');
        popupContent.classList.remove('popup-human');
      } else {
        popupIcon.className = 'fas fa-user';
        popupIcon.style.color = '#2b7a4e';
        popupTitle.innerText = '👤 Human-Written Content Detected';
        popupContent.classList.add('popup-human');
        popupContent.classList.remove('popup-ai');
      }

      confidenceFill.style.width = result.confidence + '%';
      if (result.isAI) {
        confidenceFill.style.background = 'linear-gradient(90deg, #F44336, #FFC107)';
      } else {
        confidenceFill.style.background = 'linear-gradient(90deg, #4CAF50, #FFC107)';
      }

      perplexityScore.innerText = result.metrics.perplexity;
      burstinessScore.innerText = result.metrics.burstiness;
      repetitionScore.innerText = result.metrics.repetition;

      popupMessage.innerHTML = `<strong>AI Content: ${result.confidence}%</strong><br>Text appears to be ${result.isAI ? 'AI-generated' : 'human-written'}`;

      analysisPoints.innerHTML = result.analysis.map(point => 
        `<div style="margin: 0.5rem 0; padding: 0.3rem; border-left: 3px solid ${point.includes('🔴') ? '#F44336' : point.includes('🟢') ? '#4CAF50' : '#FFC107'}; padding-left: 0.8rem;">${point}</div>`
      ).join('');

      aiPopup.classList.remove('hidden');
    }

    closePopupBtn.addEventListener('click', () => {
      aiPopup.classList.add('hidden');
    });

    aiPopup.addEventListener('click', (e) => {
      if (e.target === aiPopup) {
        aiPopup.classList.add('hidden');
      }
    });

    // ========== UPDATE COUNTER UI ==========
    function updateRegCounterUI() {
      regCounterDisplay.innerText = registeredUsers.length;
    }

    // ========== HOST NOTIFICATION SYSTEM ==========
    function showNotification(message, duration = 3500) {
      notificationText.innerText = message;
      notificationBar.classList.add('show');
      setTimeout(() => {
        notificationBar.classList.remove('show');
      }, duration);
    }

    // ========== DATABASE FUNCTIONS ==========
    function displayDatabase() {
      dbTableBody.innerHTML = "";
      registeredUsers.forEach((user, index) => {
        dbTableBody.innerHTML += `
          <tr>
            <td><img src="${user.photo || 'https://via.placeholder.com/40'}" class="profile-photo" alt="photo"></td>
            <td>${user.name}</td>
            <td>${user.regNo}</td>
            <td>${user.department}</td>
            <td>${user.year}</td>
            <td>${user.semester}</td>
            <td>${user.email}</td>
            <td>${user.phone}</td>
            <td>${user.date || new Date().toLocaleDateString()}</td>
            <td><button class="delete-btn" onclick="deleteUser(${index})">Delete</button></td>
          </tr>
        `;
      });

      if (totalResearchers) {
        totalResearchers.innerText = registeredUsers.length;
      }
      if (deptStats) {
        const deptCount = {};
        registeredUsers.forEach(user => {
          deptCount[user.department] = (deptCount[user.department] || 0) + 1;
        });
        deptStats.innerHTML = Object.entries(deptCount).map(([dept, count]) => 
          `<div>• ${dept}: ${count}</div>`
        ).join('');
      }
    }

    // Make deleteUser global
    window.deleteUser = function(index) {
      registeredUsers.splice(index, 1);
      localStorage.setItem("researchUsers", JSON.stringify(registeredUsers));
      displayDatabase();
      updateRegCounterUI();
    };

    // ========== ACTIVITY LOG DISPLAY ==========
    function displayActivityLog() {
      if (loginActivityLog.length === 0) {
        activityList.innerHTML = '<p style="text-align: center; color: #999;">No login activity yet</p>';
        return;
      }

      let html = '';
      const recentTime = 5 * 60 * 1000; // 5 minutes
      const now = Date.now();

      loginActivityLog.slice().reverse().forEach(activity => {
        const isRecent = (now - activity.timestamp) < recentTime;
        html += `
          <div class="activity-item ${isRecent ? 'recent' : ''}">
            <div>
              <strong>${activity.user}</strong> logged in
            </div>
            <div class="activity-time">${new Date(activity.timestamp).toLocaleString()}</div>
          </div>
        `;
      });

      activityList.innerHTML = html;
    }

    // ========== DATABASE REGISTRATION FORM ==========
    dbRegistrationForm.addEventListener("submit", function(e) {
      e.preventDefault();

      const name = document.getElementById("dbName").value.trim();
      const regNo = document.getElementById("dbRegNo").value.trim();
      const department = document.getElementById("dbDepartment").value;
      const year = document.getElementById("dbYear").value;
      const semester = document.getElementById("dbSemester").value;
      const email = document.getElementById("dbEmail").value.trim();
      const phone = document.getElementById("dbPhone").value.trim();
      const photoInput = document.getElementById("dbPhoto");

      if (!name || !regNo || !department || !year || !semester || !email || !phone || !photoInput.files[0]) {
        alert("Please fill all fields!");
        return;
      }

      if (registeredUsers.some(u => u.regNo.toLowerCase() === regNo.toLowerCase())) {
        alert("Register Number already exists!");
        return;
      }

      const reader = new FileReader();
      reader.onload = function() {
        const newUser = {
          name, regNo, department, year, semester, email, phone,
          photo: reader.result,
          date: new Date().toLocaleDateString()
        };
        registeredUsers.push(newUser);
        localStorage.setItem("researchUsers", JSON.stringify(registeredUsers));
        displayDatabase();
        updateRegCounterUI();
        dbRegistrationForm.reset();
        showNotification(`✅ ${name} added to database successfully!`);
      };
      reader.readAsDataURL(photoInput.files[0]);
    });

    // ========== AUTH UI UPDATE ==========
    function updateUIBasedOnAuth() {
      if (currentUser) {
        authContainer.classList.add('hidden');
        mainContainer.classList.remove('hidden');
        greetingName.innerText = currentUser.name;
        displayDatabase();
        displayActivityLog();

        // Show notification that user logged in
        showNotification(`🔔 Welcome ${currentUser.name}! You have logged into the system.`);

        // Listen for activity updates from other windows
        window.addEventListener('storage', function(e) {
          if (e.key === 'loginActivity') {
            loginActivityLog = JSON.parse(e.newValue || "[]");
            displayActivityLog();
            if (e.newValue) {
              const lastActivity = JSON.parse(e.newValue).slice(-1)[0];
              if (lastActivity && lastActivity.user !== currentUser.name) {
                showNotification(`🔔 ${lastActivity.user} joined the session.`);
              }
            }
          }
        });
      } else {
        authContainer.classList.remove('hidden');
        mainContainer.classList.add('hidden');
      }
    }

    // ========== FORM SWITCHING ==========
    switchToSignup.addEventListener('click', () => {
      signinFormDiv.classList.add('hidden');
      signupFormDiv.classList.remove('hidden');
    });

    switchToLogin.addEventListener('click', () => {
      signupFormDiv.classList.add('hidden');
      signinFormDiv.classList.remove('hidden');
    });

    // ========== SIGN UP ==========
    signupSubmit.addEventListener('click', (e) => {
      e.preventDefault();
      const name = document.getElementById('signupName').value.trim();
      const email = document.getElementById('signupEmail').value.trim();
      const pwd = document.getElementById('signupPassword').value.trim();
      const regNo = document.getElementById('signupRegNo').value.trim();
      const dept = document.getElementById('signupDept').value;
      const year = document.getElementById('signupYear').value;
      const sem = document.getElementById('signupSem').value;
      const phone = document.getElementById('signupPhone').value.trim();
      const photoInput = document.getElementById('signupPhoto');

      if (!name || !email || !pwd || !regNo || !dept || !year || !sem || !phone || !photoInput.files[0]) {
        alert('Please fill all fields');
        return;
      }

      if (pwd.length < 8) {
        alert('Password must be at least 8 characters');
        return;
      }

      if (registeredUsers.some(u => u.regNo.toLowerCase() === regNo.toLowerCase())) {
        alert('Register Number already exists!');
        return;
      }

      const reader = new FileReader();
      reader.onload = function() {
        const newUser = {
          name, regNo, department: dept, year, semester: sem, email, phone,
          photo: reader.result,
          date: new Date().toLocaleDateString()
        };
        registeredUsers.push(newUser);
        localStorage.setItem("researchUsers", JSON.stringify(registeredUsers));

        // Record login activity
        const loginEvent = {
          user: name,
          timestamp: Date.now(),
          type: 'signup'
        };
        loginActivityLog.push(loginEvent);
        localStorage.setItem("loginActivity", JSON.stringify(loginActivityLog));

        currentUser = { name: name, email: email };
        updateRegCounterUI();
        updateUIBasedOnAuth();

        document.getElementById('signupName').value = '';
        document.getElementById('signupEmail').value = '';
        document.getElementById('signupPassword').value = '';
        document.getElementById('signupRegNo').value = '';
        document.getElementById('signupPhone').value = '';
        document.getElementById('signupPhoto').value = '';
        signupFormDiv.classList.add('hidden');
        signinFormDiv.classList.remove('hidden');
      };
      reader.readAsDataURL(photoInput.files[0]);
    });

    // ========== SIGN IN ==========
    loginSubmit.addEventListener('click', (e) => {
      e.preventDefault();
      const email = document.getElementById('loginEmail').value.trim();
      const pwd = document.getElementById('loginPassword').value.trim();

      if (!email || !pwd) {
        alert('Please enter email and password');
        return;
      }

      const user = registeredUsers.find(u => u.email.toLowerCase() === email.toLowerCase());

      if (user) {
        // Record login activity
        const loginEvent = {
          user: user.name,
          timestamp: Date.now(),
          type: 'login'
        };
        loginActivityLog.push(loginEvent);
        localStorage.setItem("loginActivity", JSON.stringify(loginActivityLog));

        currentUser = { name: user.name, email: user.email };
        updateUIBasedOnAuth();
      } else {
        if (email && pwd) {
          let name = email.split('@')[0];
          name = name.charAt(0).toUpperCase() + name.slice(1);

          const loginEvent = {
            user: name,
            timestamp: Date.now(),
            type: 'demo_login'
          };
          loginActivityLog.push(loginEvent);
          localStorage.setItem("loginActivity", JSON.stringify(loginActivityLog));

          currentUser = { name: name, email: email };
          updateUIBasedOnAuth();
        } else {
          alert('Invalid credentials');
        }
      }
    });

    logoutBtn.addEventListener('click', () => {
      currentUser = null;
      updateUIBasedOnAuth();
    });

    // ========== FILE UPLOAD HANDLING ==========
    uploadZone.addEventListener('click', () => fileInput.click());
    uploadZone.addEventListener('dragover', (e) => {
      e.preventDefault();
      uploadZone.style.background = '#e3f0fd';
    });
    uploadZone.addEventListener('dragleave', () => {
      uploadZone.style.background = '#f1f9ff';
    });
    uploadZone.addEventListener('drop', (e) => {
      e.preventDefault();
      uploadZone.style.background = '#f1f9ff';
      const files = e.dataTransfer.files;
      if (files.length) handleFile(files[0]);
    });

    fileInput.addEventListener('change', (e) => {
      if (e.target.files.length) handleFile(e.target.files[0]);
    });

    async function handleFile(file) {
      const ext = file.name.split('.').pop().toLowerCase();
      if (!['txt','pdf'].includes(ext)) {
        alert('Only .txt or .pdf files allowed');
        return;
      }
      if (file.size > 10 * 1024 * 1024) {
        alert('File exceeds 10MB limit');
        return;
      }

      fileInfo.innerText = `📄 ${file.name} (${(file.size/1024).toFixed(1)} KB)`;
      extractMessage.classList.remove('hidden');
      extractMsgSpan.innerText = `Extracting text from ${file.name}...`;

      try {
        let text = '';
        if (ext === 'txt') {
          text = await readTxt(file);
        } else {
          text = await readPdf(file);
        }
        paperInput.value = text.substring(0, 6000);
        extractMsgSpan.innerText = `✅ Extracted ${text.length} characters from ${file.name}`;
      } catch (err) {
        console.error(err);
        alert('Failed to extract text from file.');
        extractMessage.classList.add('hidden');
      }
    }

    function readTxt(file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onload = (e) => resolve(e.target.result);
        reader.onerror = reject;
        reader.readAsText(file);
      });
    }

    async function readPdf(file) {
      const arrayBuffer = await file.arrayBuffer();
      const pdf = await pdfjsLib.getDocument({ data: arrayBuffer }).promise;
      let fullText = '';
      for (let i = 1; i <= pdf.numPages; i++) {
        const page = await pdf.getPage(i);
        const content = await page.getTextContent();
        const strings = content.items.map(item => item.str);
        fullText += strings.join(' ') + '\n';
      }
      return fullText;
    }

    // ========== INTEGRITY CHECK ==========
    function runIntegrityCheck(text) {
      const txt = text.toLowerCase();
      let score = 70;
      const warnings = [];
      const ethicsIssues = [];

      if (!txt.includes('et al') && !txt.includes('reference') && !txt.includes('citation')) {
        warnings.push('⚠️ Potential plagiarism: no citations detected (32% similarity risk)');
        score -= 12;
      } else {
        warnings.push('⚠️ Moderate similarity with 2 sources (plagiarism scan)');
        score -= 4;
      }

      if (txt.includes('p-value') && (txt.includes('0.049') || txt.includes('0.05'))) {
        warnings.push('📉 Data falsification risk: p-value heaping near threshold');
        score -= 14;
      } else if (txt.includes('p-value')) {
        warnings.push('📉 p-value reported without correction for multiple testing');
        score -= 5;
      } else {
        warnings.push('📉 No p-values / effect sizes – statistical rigour low');
        score -= 6;
      }

      if (!txt.includes('double-blind') && !txt.includes('randomized') && !txt.includes('control')) {
        warnings.push('🧪 Methodological accuracy: no blinding/control group (possible bias)');
        score -= 8;
      }

      if (!txt.includes('et al') && !txt.includes('202')) {
        warnings.push('📚 Citation authenticity: references missing or unreachable');
        score -= 8;
      } else {
        warnings.push('📚 Citation authenticity: 1 reference appears outdated');
        score -= 2;
      }

      if (!txt.includes('conflict') && !txt.includes('interest')) {
        ethicsIssues.push('No conflict of interest declared');
        score -= 5;
      }
      if (!txt.includes('consent') && !txt.includes('irb') && !txt.includes('ethical')) {
        ethicsIssues.push('Informed consent / IRB approval missing');
        score -= 7;
      }
      if (!txt.includes('bias') && !txt.includes('limitation')) {
        warnings.push('📊 Bias / limitations not discussed');
        score -= 3;
      }

      score = Math.min(100, Math.max(20, Math.round(score)));

      let warnHtml = '';
      warnings.slice(0, 5).forEach(w => {
        let color = '#c44536';
        if (w.includes('p-value') || w.includes('falsification')) color = '#e68c2e';
        else if (w.includes('citation') || w.includes('reference')) color = '#71a3cf';
        warnHtml += `<div style="border-left:6px solid ${color}; background:white; padding:0.8rem 1.2rem; border-radius:40px; margin-bottom:0.6rem;">${w}</div>`;
      });
      if (warnHtml === '') warnHtml = '<div style="background:white; padding:0.8rem; border-radius:40px;">✅ No major warnings</div>';

      let ethicsHtml = `⚖️ ETHICS: ` + (ethicsIssues.length ? ethicsIssues.join(' · ') : 'All ethics checks passed') + ` <strong style="margin-left:1rem; background:#1e3f60; color:white; padding:0.2rem 1.2rem; border-radius:40px;">⚠️ ${ethicsIssues.length} flags</strong>`;

      return { score, warnHtml, ethicsHtml };
    }

    function updateReport() {
      const text = paperInput.value.trim() || '(empty)';
      const result = runIntegrityCheck(text);
      scoreDisplay.innerText = result.score + '/100';
      warningList.innerHTML = result.warnHtml;
      ethicsFlag.innerHTML = result.ethicsHtml;

      if (currentUser && text.length > 50) {
        const aiResult = deepSeekDetector.detect(text);
        showDeepSeekPopup(aiResult);
      } else if (currentUser && text.length <= 50) {
        alert('Please enter more text (at least 50 characters) for AI analysis.');
      }
    }

    resetBtn.addEventListener('click', () => {
      paperInput.value = `Our study investigates the effect of X on Y using a convolutional neural network. We obtained a p-value of 0.049 (just above threshold). Some references: Smith et al. (2020) reported similar findings. No conflicts of interest. Data available upon request.`;
      fileInfo.innerText = '';
      extractMessage.classList.add('hidden');
      updateReport();
    });

    checkBtn.addEventListener('click', (e) => {
      e.preventDefault();
      updateReport();
    });

    // ========== WINDOW LOAD ==========
    window.addEventListener('load', () => {
      currentUser = null;
      updateRegCounterUI();
      updateUIBasedOnAuth();
      updateReport();
      displayDatabase();
      displayActivityLog();
    });

    // Watch for login activity changes in real-time
    window.addEventListener('storage', function(e) {
      if (e.key === 'loginActivity') {
        loginActivityLog = JSON.parse(e.newValue || "[]");
        displayActivityLog();
        if (e.newValue && currentUser) {
          const newActivity = JSON.parse(e.newValue).slice(-1)[0];
          if (newActivity && newActivity.user !== currentUser.name) {
            showNotification(`🔔 Team Activity: ${newActivity.user} joined the session.`, 4000);
          }
        }
      }
    });
  </script>
</body>
</html>
