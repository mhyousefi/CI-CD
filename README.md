# XO Game - Tic Tac Toe

A real-time multiplayer Tic Tac Toe (XO) game built with Node.js, Express, and Socket.IO.

## 🎮 Features

- **Real-time multiplayer gameplay** using Socket.IO
- **Beautiful, responsive UI** with modern design
- **Game sharing** - share game links with friends
- **Cross-platform** - works on desktop and mobile
- **Automatic game state management**
- **Win detection** for all possible combinations
- **Draw detection** when board is full

## 🚀 Quick Start

### Prerequisites

- Node.js (version 16 or higher)
- npm or yarn

### Installation

1. Clone the repository:
```bash
git clone <https://github.com/HatemMohmmed73/CI-CD>
cd xo-game
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

4. Open your browser and navigate to `http://localhost:3000`

### Production

To run in production mode:
```bash
npm start
```

## 🧪 Testing

Run the test suite:
```bash
npm test
```

Run tests with coverage:
```bash
npm test -- --coverage
```

Run linting:
```bash
npm run lint
```

Fix linting issues:
```bash
npm run lint:fix
```

## 📁 Project Structure

```
xo-game/
├── server.js              # Main server file
├── package.json           # Dependencies and scripts
├── public/                # Static files
│   ├── index.html        # Main game page
│   ├── style.css         # Game styles
│   └── script.js         # Client-side logic
├── tests/                 # Test files
│   ├── game.test.js      # Game logic tests
│   ├── server.test.js    # Server endpoint tests
│   └── setup.js          # Test setup
├── .github/workflows/     # CI/CD workflows
│   └── ci-cd.yml         # GitHub Actions pipeline
└── README.md             # This file
```

## 🔧 Configuration

The game can be configured through environment variables:

- `PORT`: Server port (default: 3000)
- `NODE_ENV`: Environment mode (development/production)

## 🎯 How to Play

1. **Start a game**: Open the application in your browser
2. **Share the game**: Click "Share Game" to get a link
3. **Invite a friend**: Send the link to someone to join
4. **Take turns**: Players alternate placing X and O
5. **Win**: Get three in a row (horizontally, vertically, or diagonally)
6. **New game**: Click "New Game" to start over

## 🚀 CI/CD Pipeline

This project includes a comprehensive GitHub Actions CI/CD pipeline with the following stages:

### 1. Test and Lint
- Runs on multiple Node.js versions (16.x, 18.x, 20.x)
- Executes unit tests and integration tests
- Runs ESLint for code quality
- Uploads coverage reports to Codecov

### 2. Build
- Verifies the application builds correctly
- Creates build artifacts
- Ensures all dependencies are properly resolved

### 3. Security Scan
- Runs npm audit for vulnerability scanning
- Integrates with Snyk for advanced security analysis
- Fails the pipeline on high-severity issues

### 4. Deployment
- **Staging**: Deploys to staging environment on `develop` branch
- **Production**: Deploys to production environment on `main` branch
- Includes deployment notifications

### 5. Notifications
- Sends success/failure notifications
- Provides pipeline status updates

## 🔍 API Endpoints

- `GET /` - Serves the main game page
- `GET /health` - Health check endpoint
- `GET /style.css` - Game styles
- `GET /script.js` - Client-side JavaScript

## 🧪 Testing Strategy

- **Unit Tests**: Test individual game logic functions
- **Integration Tests**: Test server endpoints and Socket.IO events
- **Coverage**: Aim for >80% code coverage
- **Linting**: ESLint ensures code quality and consistency

## 🛠️ Development

### Adding New Features

1. Create a feature branch
2. Write tests for new functionality
3. Implement the feature
4. Ensure all tests pass
5. Run linting: `npm run lint`
6. Submit a pull request

### Code Style

This project uses ESLint with the following rules:
- 2-space indentation
- Single quotes for strings
- Semicolons required
- Unix line endings

## 📊 Monitoring

The application includes:
- Health check endpoint (`/health`)
- Real-time connection monitoring
- Game state tracking
- Error logging

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Ensure all tests pass
6. Submit a pull request

## 📄 License

This project is licensed under the MIT License.

## 🆘 Support

If you encounter any issues:
1. Check the console for error messages
2. Ensure all dependencies are installed
3. Verify Node.js version compatibility
4. Check the GitHub Actions logs for CI/CD issues

---

**Happy Gaming! 🎮** 
