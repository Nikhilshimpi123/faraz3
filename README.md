# faraz3
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Pathology Management - Nikhil Shimpi</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: url('https://images.unsplash.com/photo-1588776814546-ec9e75aaed7e') no-repeat center center fixed;
      background-size: cover;
      color: #fff;
    }
    header {
      background-color: rgba(0, 51, 102, 0.9);
      padding: 1rem;
      text-align: center;
      font-size: 2rem;
      font-weight: bold;
      color: #fff;
    }
    .container {
      max-width: 1000px;
      margin: 2rem auto;
      padding: 1rem;
      background-color: rgba(255, 255, 255, 0.9);
      border-radius: 10px;
      color: #000;
    }
    h2 {
      background: #0066cc;
      color: white;
      padding: 0.5rem;
      border-radius: 5px;
    }
    .profile-card {
      border: 2px solid #0066cc;
      border-radius: 10px;
      padding: 1rem;
      margin: 1rem 0;
      background-color: #f9f9f9;
    }
    .profile-card button {
      padding: 0.5rem 1rem;
      background-color: #0066cc;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      margin-top: 0.5rem;
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
      gap: 1rem;
    }
    label {
      display: flex;
      justify-content: space-between;
      background-color: #e0f7fa;
      padding: 0.5rem;
      border-radius: 5px;
      margin-bottom: 0.5rem;
    }
    .total {
      margin-top: 1rem;
      font-weight: bold;
      font-size: 1.2rem;
    }
    form {
      background-color: #e6f2ff;
      padding: 1rem;
      border-radius: 10px;
      margin-bottom: 2rem;
    }
    form label {
      display: block;
      margin: 0.5rem 0;
    }
    form input, form select {
      width: 100%;
      padding: 0.5rem;
      margin-top: 0.3rem;
    }
    form button {
      background-color: #0066cc;
      color: white;
      padding: 0.5rem 1rem;
      border: none;
      border-radius: 5px;
      margin-top: 1rem;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <header>Pathology Management - Nikhil Shimpi</header>
  <div class="container">
    <h2>Patient Registration</h2>
    <form>
      <label>Name: <input type="text" name="name" required /></label>
      <label>Age: <input type="number" name="age" required /></label>
      <label>Gender:
        <select name="gender">
          <option value="male">Male</option>
          <option value="female">Female</option>
          <option value="other">Other</option>
        </select>
      </label>
      <label>Phone: <input type="tel" name="phone" required /></label>
      <label>Email: <input type="email" name="email" /></label>
      <button type="submit">Register</button>
    </form>

    <h2>Test Profiles</h2>
    <div class="profile-card">
      <strong>Profile 1:</strong> CBC, ESR, Calcium, R.A. Test, Uric Acid, Vitamin B12, Vitamin D3<br />
      Price: ₹2130<br />
      <button onclick="window.open('profile1.html', '_blank')">Select Profile 1</button>
    </div>
    <div class="profile-card">
      <strong>Profile 2:</strong> CBC, Fasting Blood Sugar, Post Prandial Sugar, Kidney Profile, HbA1c, Calcium<br />
      Price: ₹1100<br />
      <button onclick="window.open('profile2.html', '_blank')">Select Profile 2</button>
    </div>
    <div class="profile-card">
      <strong>Profile 3:</strong> CBC, Fasting Sugar, Post Prandial Sugar, Liver Function Test, Thyroid Profile, HbA1c<br />
      Price: ₹1399<br />
      <button onclick="window.open('profile3.html', '_blank')">Select Profile 3</button>
    </div>
    <div class="profile-card">
      <strong>Profile 4:</strong> CBC, Thyroid Profile, HbA1c, Lipid Profile, Liver Function Test, Kidney Function Test, Vitamin B12, Vitamin D<br />
      Price: ₹3420<br />
      <button onclick="window.open('profile4.html', '_blank')">Select Profile 4</button>
    </div>

    <h2>Profile 5 - Custom Test Selection</h2>
    <div class="grid" id="testList"></div>
    <div class="total">Total: ₹<span id="totalAmount">0</span></div>
  </div>

  <script>
    const tests = [
      { name: 'CBC', price: 200 },
      { name: 'Blood Group', price: 80 },
      { name: 'F/P P Sugar', price: 100 },
      { name: 'ESR', price: 100 },
      { name: 'Calcium', price: 300 },
      { name: 'R.A. Test', price: 200 },
      { name: 'Uric Acid', price: 150 },
      { name: 'Vitamin B12', price: 1500 },
      { name: 'Vitamin D3', price: 1300 },
      { name: 'Kidney Function Test (KFT)', price: 500 },
      { name: 'Liver Function Test (LFT)', price: 500 },
      { name: 'Thyroid Profile', price: 500 },
      { name: 'Lipid Profile', price: 800 },
      { name: 'Semen Test', price: 400 },
      { name: 'HbA1c', price: 500 },
      { name: 'Blood Urea', price: 150 },
      { name: 'Serum Electrolyte', price: 400 },
      { name: 'Serum Creatinine', price: 150 }
    ];

    const testList = document.getElementById('testList');
    const totalAmount = document.getElementById('totalAmount');

    tests.forEach((test, index) => {
      const label = document.createElement('label');
      const checkbox = document.createElement('input');
      checkbox.type = 'checkbox';
      checkbox.dataset.price = test.price;
      checkbox.addEventListener('change', updateTotal);
      label.appendChild(checkbox);
      label.append(` ${test.name} (₹${test.price})`);
      testList.appendChild(label);
    });

    function updateTotal() {
      const checkboxes = document.querySelectorAll('input[type="checkbox"]');
      let total = 0;
      checkboxes.forEach(cb => {
        if (cb.checked) total += Number(cb.dataset.price);
      });
      totalAmount.textContent = total;
    }
  </script>
</body>
</html>
