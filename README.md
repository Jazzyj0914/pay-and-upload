# pay-and-upload
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Payment and Upload</title>
</head>
<body>
    <h1>Payment and Upload</h1>
    
    <form id="payment-form">
        <!-- Other form fields -->
        <label for="video-url-field">Video URL:</label>
        <input type="text" id="video-url-field" name="video-url" placeholder="Enter video URL">

        <!-- Pay and Upload Button -->
        <button type="button" id="pay-and-upload-button">Pay $3 and Upload</button>
    </form>

    <script>
        // Function to handle payment processing and navigate to Stripe Checkout
        function processPaymentAndNavigate() {
            // Navigate to Stripe Checkout for payment (https://buy.stripe.com/3cs3fP0ev64NeE8aEE)
            window.location.href = 'https://buy.stripe.com/3cs3fP0ev64NeE8aEE';
        }

        // Function to handle video upload after payment is confirmed
        function uploadVideo() {
            // Get the video URL from the video URL field
            var videoUrl = document.getElementById('video-url-field').value;

            // Simulate upload process (upload video to watch and earn)
            console.log('Uploading video from URL:', videoUrl);
            console.log('Video uploaded successfully.');
            // Navigate to the "watch and earn" page (https://a.picoapps.xyz/employee-political)
            window.location.href = 'https://yourwebsite.com/watch-and-earn';
        }

        // Event listener for when the pay $3 and upload button is clicked
        document.getElementById('pay-and-upload-button').addEventListener('click', function() {
            // Process payment and navigate to Stripe Checkout
            processPaymentAndNavigate();
        });

        // Simulated function to check payment confirmation (removed setTimeout)
        /*
        function checkPaymentConfirmation() {
            // Simulated check for payment confirmation (once payment is approved)
    
                // Simulated payment confirmed
                // Proceed with video upload
                uploadVideo();
            }, 3000); // Simulate payment confirmation after 3 seconds
        }
        */

        // Call the function to check payment confirmation (removed)
        // This function should be called after the user is redirected back to your website from the payment page
        // checkPaymentConfirmation();
    </script>
</body>
</html>
<!DOCTYPE html>
const express = require('express');
const bodyParser = require('body-parser');
const stripe = require('stripe')('sk_live_...AxFR');

const app = express();
const port = process.env.PORT || 3000;

// Parse JSON bodies
app.use(bodyParser.json());

// Endpoint to handle incoming webhook events from Stripe
app.post('/stripe-webhook', async (req, res) => {
  const sig = req.headers['stripe-signature'];
  let event;

  try {
    event = stripe.webhooks.constructEvent(req.body, sig, 'whsec_rfXz4SiM9BeikFtAO4NShiRerhrZ0GFH');
  } catch (err) {
    console.error('Webhook signature verification failed.', err);
    return res.status(400).send('Webhook Error: Signature Verification Failed');
  }

  // Handle the event
  switch (event.type) {
    case 'payment_intent.succeeded':
      const paymentIntent = event.data.object;
      // Handle successful payment confirmation
      console.log('Payment confirmation received:', paymentIntent);
      break;
    case 'payment_intent.failed':
      const failedPaymentIntent = event.data.object;
      // Handle failed payment
      break;
    // Handle other event types as needed
    default:
      console.log(`Unhandled event type ${event.type}`);
  }

  res.status(200).end();
});

// Start the server
app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
