# pay-and-upload
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
