# Vibe Codes AI Images 🎨

Generate stunning images from text prompts using OpenAI's DALL-E 3 API. A modern web application that transforms your creative ideas into visual art.

## ✨ Features

- **AI-Powered Image Generation**: Uses OpenAI DALL-E 3 for high-quality image creation
- **Prompt Suggestions**: Get inspired with pre-built prompt templates
- **Multiple Image Sizes**: Generate square, landscape, or portrait images
- **HD Quality Option**: Create images at standard or HD resolution
- **Image Gallery**: View and manage your generated images
- **Download Images**: Save generated images to your device
- **Copy Prompts**: Quick copy to clipboard for easy sharing
- **Responsive Design**: Works seamlessly on desktop, tablet, and mobile
- **Image History**: View all your previously generated images

## 🛠️ Tech Stack

### Frontend
- **React 18** - Modern UI library
- **TypeScript** - Type safety
- **Tailwind CSS** - Utility-first styling
- **Vite** - Lightning-fast build tool
- **Axios** - HTTP client

### Backend
- **Node.js** - JavaScript runtime
- **Express.js** - Web framework
- **OpenAI API** - DALL-E 3 integration
- **CORS** - Cross-origin support

## 🚀 Quick Start

### Prerequisites
- Node.js 16+ and npm
- OpenAI API Key ([Get it here](https://platform.openai.com/api-keys))

### Installation

1. **Clone the repository**:
```bash
git clone https://github.com/bats314159/Vibe-Codes-AI-Images.git
cd Vibe-Codes-AI-Images
```

2. **Install dependencies**:
```bash
npm install
cd client && npm install && cd ..
cd server && npm install && cd ..
```

3. **Configure environment** (see SETUP.md for detailed guide):
```bash
cp server/.env.example server/.env
# Edit server/.env and add your OpenAI API key
```

4. **Run development server**:
```bash
npm run dev
```

Visit:
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:5000

## 📁 Project Structure

```
Vibe-Codes-AI-Images/
├── client/                 # React frontend
│   ├── src/
│   │   ├── components/    # React components
│   │   ├── App.jsx        # Main app
│   │   └── main.jsx       # Entry point
│   └── package.json
├── server/                 # Express backend
│   ├── index.js           # API server
│   ├── .env.example       # Environment template
│   └── package.json
├── README.md              # This file
├── SETUP.md               # Detailed setup guide
└── DEPLOYMENT.md          # Deployment instructions
```

## 📖 Documentation

- **[SETUP.md](./SETUP.md)** - Complete setup and troubleshooting guide
- **[DEPLOYMENT.md](./DEPLOYMENT.md)** - Deploy to production

## 🎯 How to Use

1. **Enter a Prompt**: Describe the image you want to generate
2. **Choose Size**: Select from square, landscape, or portrait
3. **Select Quality**: Choose standard or HD quality
4. **Generate**: Click "Generate Image" and wait for the magic
5. **Download**: Save your generated image
6. **Share**: Copy the prompt and share with friends

## 💡 Example Prompts

- "A serene mountain landscape at sunset with golden light"
- "A futuristic city skyline with neon lights at night"
- "A cozy coffee shop with warm lighting and plants"
- "An abstract colorful pattern with geometric shapes"
- "A peaceful forest stream with moss-covered rocks"

## 🔐 Environment Variables

### Backend (server/.env)
```
OPENAI_API_KEY=your_key_here
PORT=5000
NODE_ENV=development
CLIENT_URL=http://localhost:3000
```

### Frontend (.env) - Optional
```
VITE_API_URL=http://localhost:5000
```

## 📊 API Reference

### Generate Image
```
POST /api/generate
Content-Type: application/json

{
  "prompt": "A beautiful sunset",
  "size": "1024x1024",
  "quality": "standard",
  "n": 1
}

Response:
{
  "success": true,
  "imageUrl": "https://...",
  "prompt": "A beautiful sunset",
  "timestamp": "2026-05-02T..."
}
```

## 🌐 Deployment

Deploy to production using:
- **Vercel** (Frontend) - Free tier available
- **Render** (Backend) - Free tier available
- **Heroku** (Backend) - Paid
- **AWS** (Production grade)

See [DEPLOYMENT.md](./DEPLOYMENT.md) for detailed instructions.

## 💰 Pricing

DALL-E 3 API pricing:
- **Standard**: $0.040 per image (1024×1024)
- **HD**: $0.080 per image (1024×1024)

[View OpenAI Pricing](https://openai.com/pricing)

## 🐛 Troubleshooting

### "Invalid API Key"
- Verify your OpenAI API key is correct
- Check it's not expired or revoked
- Ensure it's in `server/.env`

### "Rate limit exceeded"
- OpenAI has rate limits based on your plan
- Wait before making new requests
- Upgrade your OpenAI plan for higher limits

### "CORS Error"
- Ensure `CLIENT_URL` in backend matches your frontend URL
- Frontend and backend must be on same or whitelisted origins

### "Port already in use"
- Change port in `server/index.js`
- Or kill the process using the port

See [SETUP.md](./SETUP.md) for more troubleshooting.

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest features
- Submit pull requests
- Improve documentation

## 📝 License

This project is open source and available under the MIT License.

## 🙏 Credits

- Built with [React](https://react.dev)
- Powered by [OpenAI DALL-E 3](https://openai.com/dall-e-3)
- Styled with [Tailwind CSS](https://tailwindcss.com)
- Deployed with [Vercel](https://vercel.com) & [Render](https://render.com)

## 📧 Support

For issues or questions:
- Check [SETUP.md](./SETUP.md) for common problems
- Review [DEPLOYMENT.md](./DEPLOYMENT.md) for deployment help
- Open an issue on GitHub

## 🚀 Getting Started Now

1. Get your OpenAI API key: https://platform.openai.com/api-keys
2. Follow the [SETUP.md](./SETUP.md) guide
3. Run `npm run dev`
4. Start creating! 🎨

---

**Happy image generating!** ✨

*Vibe Codes AI Images - Turn Your Words Into Art*
