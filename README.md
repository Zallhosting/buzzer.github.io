# buzzer.github.io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Website Top-Up</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 0;
        }

        .container {
            width: 50%;
            margin: 50px auto;
            padding: 20px;
            background-color: #fff;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
        }

        h2 {
            text-align: center;
            color: #333;
        }

        label {
            display: block;
            margin: 10px 0 5px;
        }

        select, input, button {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            border-radius: 5px;
            border: 1px solid #ddd;
        }

        button {
            background-color: #4CAF50;
            color: white;
            cursor: pointer;
        }

        button:hover {
            background-color: #45a049;
        }

        .message {
            text-align: center;
            color: green;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div class="container">
        <h2>Top-Up Saldo</h2>
        <form id="topUpForm">
            <label for="amount">Pilih Jumlah Top-Up:</label>
            <select id="amount" name="amount" required>
                <option value="10000">Rp 10.000</option>
                <option value="20000">Rp 20.000</option>
                <option value="50000">Rp 50.000</option>
                <option value="100000">Rp 100.000</option>
            </select>

            <label for="method">Pilih Metode Pembayaran:</label>
            <select id="method" name="method" required>
                <option value="transfer">Transfer Bank</option>
                <option value="e-wallet">E-Wallet</option>
                <option value="credit-card">Kartu Kredit</option>
            </select>

            <button type="submit">Proses Pembayaran</button>
        </form>

        <div id="message" class="message"></div>
    </div>

    <script>
        document.getElementById('topUpForm').addEventListener('submit', async function (event) {
            event.preventDefault();

            const amount = document.getElementById('amount').value;
            const method = document.getElementById('method').value;

            const response = await fetch('/process-top-up', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ amount, method })
            });

            const data = await response.json();
            const messageDiv = document.getElementById('message');

            if (data.success) {
                messageDiv.textContent = `Top-Up sebesar Rp ${data.amount} melalui ${data.method} berhasil!`;
                messageDiv.style.color = 'green';
            } else {
                messageDiv.textContent = 'Terjadi kesalahan, coba lagi!';
                messageDiv.style.color = 'red';
            }
        });
    </script>
</body>
</html>
