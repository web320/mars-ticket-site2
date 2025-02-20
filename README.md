<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mars Booking</title>
    <style>
        /* Existing styles here */
    </style>
</head>
<body>
    <!-- Existing header and main content here -->
    
    <div class="summary" id="summary">
        <h3>Booking Summary</h3>
        <p id="summaryContent"></p>
        <button onclick="editBooking()">Edit Booking</button>
        <div id="payment-options">
            <h4>Select Payment Method:</h4>
            <button onclick="showPaymentMethod('paypal')">PayPal</button>
            <button onclick="showPaymentMethod('naverpay')">Naver Pay</button>
            <button onclick="showPaymentMethod('kakaopay')">Kakao Pay</button>
            <button onclick="showPaymentMethod('bank')">Bank Transfer</button>
        </div>
        <div id="paypal-button-container" class="payment-method" style="display:none;"></div>
        <div id="naverpay-button-container" class="payment-method" style="display:none;">Naver Pay Placeholder</div>
        <div id="kakaopay-button-container" class="payment-method" style="display:none;">Kakao Pay Placeholder</div>
        <div id="bank-details" class="payment-method" style="display:none;">
            <p><strong>Bank Details:</strong><br>
            Bank Name: Martian Bank<br>
            Account Number: 1234567890<br>
            Account Holder: Mars Booking Inc.</p>
            <label for="bank-confirmed">I have transferred the payment:</label>
            <input type="checkbox" id="bank-confirmed" required>
            <button onclick="confirmBankPayment()">Confirm Payment</button>
        </div>
    </div>
    
    <!-- Existing footer here -->

    <script src="https://www.paypal.com/sdk/js?client-id=sb&currency=USD"></script>
    <script>
        function showBookingForm() {
            // Existing code to show booking form
        }

        function submitBooking() {
            // Existing logic for booking submission
            let summary = `<strong>Thank you, ${name}!</strong><br>Your trip to Mars has been booked.<br>` +
                          `<strong>Email:</strong> ${email}<br><strong>Departure:</strong> ${departure}<br>` +
                          `<strong>Payment:</strong> ₩${payment}`;

            // ... rest of the existing summary logic ...

            document.getElementById('summaryContent').innerHTML = summary;
            document.getElementById('bookingForm').style.display = 'none';
            document.getElementById('summary').style.display = 'block';
            document.getElementById('payment-options').style.display = 'block';
        }

        function editBooking() {
            // Existing edit booking logic
        }

        function showPaymentMethod(method) {
            var methods = document.getElementsByClassName('payment-method');
            for(var i = 0; i < methods.length; i++) {
                methods[i].style.display = 'none';
            }
            document.getElementById(method + '-button-container').style.display = 'block';

            if(method === 'paypal') {
                paypal.Buttons({
                    createOrder: function(data, actions) {
                        return actions.order.create({
                            purchase_units: [{
                                amount: {
                                    value: payment / 1000
                                }
                            }]
                        });
                    },
                    onApprove: function(data, actions) {
                        return actions.order.capture().then(function(details) {
                            alert('Transaction completed by ' + details.payer.name.given_name);
                        });
                    }
                }).render('#paypal-button-container');
            }
        }

        function confirmBankPayment() {
            if(document.getElementById('bank-confirmed').checked) {
                alert('Thank you for your payment! We will verify the transaction soon.');
                // Here you would typically notify your server to check the bank account for payment.
            } else {
                alert('Please confirm that you have made the bank transfer.');
            }
        }
    </script>
</body>
</html><!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mars Booking</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #1a1a2e;
            color: #fff;
            text-align: center;
        }
        header {
            background-color: #e94560;
            padding: 20px 0;
        }
        header h1 {
            margin: 0;
            font-size: 2.5em;
        }
        main {
            padding: 20px;
        }
        .cta {
            margin-top: 20px;
        }
        button {
            background-color: #0f3460;
            color: #fff;
            border: none;
            padding: 10px 20px;
            font-size: 1em;
            cursor: pointer;
            border-radius: 5px;
        }
        button:hover {
            background-color: #16213e;
        }
        footer {
            background-color: #0f3460;
            padding: 10px 0;
            margin-top: 20px;
        }
        .booking-form {
            display: none;
            margin-top: 20px;
            text-align: left;
            background-color: #16213e;
            padding: 20px;
            border-radius: 10px;
            width: 300px;
            margin: 20px auto;
        }
        .booking-form label {
            display: block;
            margin-bottom: 10px;
        }
        .booking-form input, .booking-form select, .booking-form textarea {
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
            border: none;
            border-radius: 5px;
        }
        .booking-form button {
            width: 100%;
            background-color: #e94560;
        }
        .summary {
            background-color: #0f3460;
            padding: 20px;
            border-radius: 10px;
            margin: 20px auto;
            width: 80%;
            display: none;
        }
    </style>
</head>
<body>
    <header>
        <h1>Welcome to Mars Booking</h1>
    </header>
    <main>
        <h2>Experience the Red Planet Like Never Before</h2>
        <p>Reserve your spot for an intergalactic adventure to Mars. Limited seats available!</p>
        <div class="cta">
            <button onclick="showBookingForm()">Book Your Trip Now</button>
        </div>
        <div class="booking-form" id="bookingForm">
            <h3>Booking Form</h3>
            <label for="name">Name:</label>
            <input type="text" id="name" placeholder="Enter your name" required>
            <label for="email">Email:</label>
            <input type="email" id="email" placeholder="Enter your email" required>
            <label for="departure">Departure Date:</label>
            <input type="date" id="departure" required>
            <label for="payment">Payment Amount:</label>
            <select id="payment">
                <option value="1000">₩1,000</option>
                <option value="5000">₩5,000</option>
                <option value="10000">₩10,000</option>
                <option value="20000">₩20,000</option>
                <option value="50000">₩50,000</option>
            </select>
            <label for="message">Additional Requests:</label>
            <textarea id="message" placeholder="Enter any special requests"></textarea>
            <label for="newsletter">
                <input type="checkbox" id="newsletter"> Subscribe to our newsletter
            </label>
            <label for="terms">
                <input type="checkbox" id="terms" required> I agree to the terms and conditions
            </label>
            <button onclick="submitBooking()">Submit</button>
        </div>
        <div class="summary" id="summary">
            <h3>Booking Summary</h3>
            <p id="summaryContent"></p>
            <button onclick="editBooking()">Edit Booking</button>
            <div id="paypal-button-container"></div>
        </div>
    </main>
    <footer>
        <p>&copy; 2025 Mars Booking Inc. All rights reserved.</p>
    </footer>

    <script src="https://www.paypal.com/sdk/js?client-id=sb&currency=USD"></script>
    <script>
        function showBookingForm() {
            document.getElementById('bookingForm').style.display = 'block';
            document.getElementById('summary').style.display = 'none';
        }

        function submitBooking() {
            const name = document.getElementById('name').value;
            const email = document.getElementById('email').value;
            const departure = document.getElementById('departure').value;
            const payment = document.getElementById('payment').value;
            const message = document.getElementById('message').value;
            const newsletter = document.getElementById('newsletter').checked;
            const terms = document.getElementById('terms').checked;

            if (name && email && departure && payment && terms) {
                let summary = `<strong>Thank you, ${name}!</strong><br>Your trip to Mars has been booked.<br>` +
                              `<strong>Email:</strong> ${email}<br><strong>Departure:</strong> ${departure}<br>` +
                              `<strong>Payment:</strong> ₩${payment}`;

                if (message) {
                    summary += `<br><strong>Additional Requests:</strong> ${message}`;
                }

                if (newsletter) {
                    summary += `<br>You have subscribed to the newsletter.`;
                }

                document.getElementById('summaryContent').innerHTML = summary;
                document.getElementById('bookingForm').style.display = 'none';
                document.getElementById('summary').style.display = 'block';

                paypal.Buttons({
                    createOrder: function(data, actions) {
                        return actions.order.create({
                            purchase_units: [{
                                amount: {
                                    value: payment / 1000
                                }
                            }]
                        });
                    },
                    onApprove: function(data, actions) {
                        return actions.order.capture().then(function(details) {
                            alert('Transaction completed by ' + details.payer.name.given_name);
                        });
                    }
                }).render('#paypal-button-container');

            } else {
                alert('Please fill in all required fields and agree to the terms.');
            }
        }

        function editBooking() {
            document.getElementById('summary').style.display = 'none';
            document.getElementById('bookingForm').style.display = 'block';
        }
    </script>
</body>
</html>

