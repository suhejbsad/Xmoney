[html code.txt](https://github.com/user-attachments/files/23842746/html.code.txt)
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Xmoney Dashboard</title>
  <style>
    /* General Styles */
    body {
      font-family: Arial, sans-serif;
      background-color: #f9fafb;
      margin: 0;
      padding: 0;
    }

    .container {
      padding: 24px;
      max-width: 1200px;
      margin: auto;
    }

    h1 {
      font-size: 2.5rem;
      font-weight: bold;
      margin-bottom: 1.5rem;
    }

    p {
      font-size: 1.25rem;
      margin-bottom: 1.5rem;
    }

    /* Grid */
    .grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 1.5rem;
    }

    @media (min-width: 768px) {
      .grid {
        grid-template-columns: repeat(3, 1fr);
      }
    }

    /* Card */
    .card {
      background-color: white;
      border-radius: 1.5rem;
      padding: 1.5rem;
      box-shadow: 0 10px 20px rgba(0,0,0,0.1);
    }

    .card h2 {
      font-size: 1.5rem;
      font-weight: bold;
      margin-bottom: 0.5rem;
    }

    /* Buttons */
    .btn {
      display: inline-block;
      text-decoration: none;
      color: white;
      padding: 0.5rem 1rem;
      border-radius: 1rem;
      margin-top: 1rem;
      text-align: center;
      width: 100%;
      transition: background 0.3s;
    }

    .btn-black { background-color: black; }
    .btn-green { background-color: #16a34a; }
    .btn-red   { background-color: #dc2626; }
    .btn-blue  { background-color: #2563eb; }

    /* Membership Section */
    .membership {
      margin-top: 2.5rem;
      padding: 1.5rem;
      background-color: #fef3c7;
      border-radius: 1rem;
      text-align: center;
    }

    .membership .btn {
      width: auto;
      padding: 0.75rem 1.5rem;
      font-size: 1.125rem;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Dashboard - Xmoney</h1>
    <p>Welcome to the next level of business collaboration with <strong>Xmoney</strong>. Your membership unlocks exclusive tools and services.</p>

    <div class="grid">
      <!-- 2 Logos -->
      <div class="card">
        <h2>2 Professional Logos – $5</h2>
        <p>Get 2 custom logos for your business.</p>
        <a href="https://whop.com/checkout/plan_QOybDJlOSXgGn" target="_blank" class="btn btn-black">Order Logos</a>
      </div>

      <!-- Business Ideas -->
      <div class="card">
        <h2>Business Ideas – $10</h2>
        <p>Receive unique ideas to grow your business.</p>
        <a href="https://whop.com/checkout/plan_P7lCCHZ89ZLDj" target="_blank" class="btn btn-green">Get Ideas</a>
      </div>

      <!-- Premium Video Editing -->
      <div class="card">
        <h2>Premium Video Editing (20s) – $10</h2>
        <p>High-quality 20-second marketing video for your business.</p>
        <a href="https://whop.com/checkout/plan_KHyI8qQTLoyqk" target="_blank" class="btn btn-red">Order Video</a>
      </div>
    </div>

    <!-- Membership Section -->
    <div class="membership">
      <h2>Xmoney Membership – $19.99 per business</h2>
      <p>Unlock access to the full platform, including all tools and priority support.</p>
      <a href="https://whop.com/checkout/plan_fenfmpRiZGQCn" target="_blank" class="btn btn-blue">Join Membership</a>
    </div>
  </div>
</body>
</html>
