# PMUY Subsidy Web Application

This is a simple web application developed as part of a Full Stack Internship assignment.  
It allows citizens to apply for an LPG connection under the **Pradhan Mantri Ujjwala Yojana (PMUY)** scheme.

<!DOCTYPE html>
<html>
<head>
  <title>PMUY Application</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <div class="container">
    <h1>PMUY Application Form</h1>
    <form id="appForm">
      <label>Aadhaar Number:</label>
      <input type="text" id="aadhaar" required /><br />

      <label>Full Name:</label>
      <input type="text" id="name" required /><br />

      <label>Annual Income (₹):</label>
      <input type="number" id="income" required /><br />

      <button type="submit">Apply</button>
    </form>

    <div id="result" class="output"></div>
  </div>

  <script>
    const form = document.getElementById("appForm");
    const result = document.getElementById("result");

    form.addEventListener("submit", function (e) {
      e.preventDefault();
      const aadhaar = document.getElementById("aadhaar").value.trim();
      const income = parseInt(document.getElementById("income").value.trim());

      let subsidy = 0;
      let message = "";

      if (!aadhaar || isNaN(income)) {
        result.innerHTML = "Please fill all details.";
        return;
      }

      if (income > 100000) {
        message = "❌ You are not eligible (Income > 1 Lakh)";
      } else {
        if (income === 0) subsidy = 50;
        else if (income <= 25000) subsidy = 40;
        else if (income <= 50000) subsidy = 30;
        else if (income <= 75000) subsidy = 20;
        else subsidy = 10;

        message = `✅ Application submitted!<br>
        Subsidy Eligible: <b>${subsidy}%</b><br>
        Expected Connection Date: <b>Within 7 days</b><br>
        Officer: <b>Ravi Kumar, District Officer</b>`;
      }

      result.innerHTML = message;
    });
  </script>
</body>
</html>


