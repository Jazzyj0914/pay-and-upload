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
            // Simulated check for payment confirmation (replace with your actual payment confirmation logic)
            // For demonstration purposes, we'll simulate a confirmation after 3 seconds
            setTimeout(function() {
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
const express = require('express');
const multer = require('multer'); // For handling file uploads
const fs = require('fs');

const app = express();
const upload = multer({ dest: 'uploads/' }); // Destination folder for uploaded files

// Route for handling video uploads
app.post('/upload', upload.single('video'), (req, res) => {
    // Validate and process the uploaded video file
    const videoFile = req.file;
    if (!videoFile) {
        return res.status(400).json({ error: 'No video file uploaded' });
    }

    // Save the video file to storage (e.g., filesystem)
    fs.renameSync(videoFile.path, `uploads/${videoFile.originalname}`);

    // Optionally, perform additional processing (e.g., database updates, video processing)

    // Respond with success message
    res.json({ message: 'Video uploaded successfully' });
});

// Start the server
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Video Upload</title>
</head>
<body>
    <h1>Video Upload</h1>
    
    <form id="video-upload-form" enctype="multipart/form-data">
        <input type="file" id="video-file" name="video" accept="video/*">
        <button type="button" id="upload-button">Upload Video</button>
    </form>

    <script>
        document.getElementById('upload-button').addEventListener('click', function() {
            var formData = new FormData();
            var videoFile = document.getElementById('video-file').files[0];
            formData.append('video', videoFile);

            fetch('http://localhost:3000/upload', {
                method: 'POST',
                body: formData
            })
            .then(response => {
                if (response.ok) {
                    alert('Video uploaded successfully');
                } else {
                    alert('Failed to upload video');
                }
            })
            .catch(error => {
                console.error('Error:', error);
                alert('An error occurred while uploading the video');
            });
        });
    </script>
</body>
</html>
<!-- payment.html -->
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
        <label for="video-url-field">Video URL:</label>
        <input type="text" id="video-url-field" name="video-url" placeholder="Enter video URL">
        <button type="button" id="pay-and-upload-button">Pay $3 and Upload</button>
    </form>

    <script>
        document.getElementById('pay-and-upload-button').addEventListener('click', function() {
            var videoUrl = document.getElementById('video-url-field').value;
            localStorage.setItem('videoUrl', videoUrl); // Store video URL in local storage
            processPaymentAndNavigate();
        });

        function processPaymentAndNavigate() {
            // Simulate payment processing and navigate to "watch and earn" page
            window.location.href = 'watch-and-earn.html';
        }
    </script>
</body>
</html>
<!-- watch-and-earn.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Watch and Earn</title>
</head>
<body>
    <h1>Watch and Earn</h1>
    
    <div>
        <h2>Video</h2>
        <iframe width="560" height="315" src="" frameborder="0" allowfullscreen></iframe>
    </div>

    <script>
        // Retrieve video URL from local storage
        var videoUrl = localStorage.getItem('videoUrl');
        if (videoUrl) {
            // Set the video URL in the iframe
            var iframe = document.querySelector('iframe');
            iframe.src = videoUrl;
        } else {
            // Handle case where video URL is not available
            console.error('Video URL not found in local storage');
        }
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Boost Your Social Media - Video Upload</title>
</head>
<body>
    <h1>Boost Your Social Media - Video Upload</h1>
    <form id="videoUploadForm" role="form" aria-labelledby="formTitle">
        <fieldset>
            <legend id="formTitle">Upload Your Video</legend>
            <div>
                <label for="video-url-field">Video URL:</label>
                <input type="text" id="video-url-field" name="video-url" placeholder="Enter video URL">
            </div>
            <div>
                <label for="paymentAmount">Payment Amount ($):</label>
                <input type="number" id="paymentAmount" name="paymentAmount" min="0.01" step="0.01" required aria-required="true">
            </div>
            <div>
                <button type="button" id="pay-and-upload-button">Pay $3 and Upload</button>
            </div>
        </fieldset>
    </form>

    <script>
        document.getElementById('pay-and-upload-button').addEventListener('click', function() {
            var videoUrl = document.getElementById('video-url-field').value;
            var paymentAmount = document.getElementById('paymentAmount').value;

            if (!videoUrl) {
                alert('Please enter a video URL.');
                return;
            }

            if (!paymentAmount) {
                alert('Please enter the payment amount.');
                return;
            }

            // Simulate payment processing and video upload
            processPaymentAndUpload(videoUrl, paymentAmount);
        });

        function processPaymentAndUpload(videoUrl, paymentAmount) {
            // Simulate payment processing and video upload
            console.log('Video URL:', videoUrl);
            console.log('Payment Amount:', paymentAmount);

            // Replace this with actual payment processing and video upload logic
            alert('Simulating payment and video upload...');
        }
    </script>
</body>
</html>
