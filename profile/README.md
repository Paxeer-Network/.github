# Paxeer Wallet SSO System 🚀

A revolutionary smart contract-based wallet connection system that enables seamless Single Sign-On across your entire Paxeer ecosystem.

## 🌟 Key Features

- **Seamless SSO**: Connect once, access all dApps automatically
- **Zero Gas Fees**: Leverages Paxeer's sponsored transactions
- **Auto-Connect**: Users stay connected across dApp navigation
- **Session Management**: Secure, time-based sessions with configurable duration
- **Smart Contract Based**: No reliance on external wallet providers
- **Beautiful UI**: Modern connection modal with smooth UX

## 🏗️ Architecture

### Smart Contracts
- **`PaxeerWalletManager.sol`**: Core session management and dApp registration
- **Session-based authentication**: Cryptographic signatures for security
- **dApp registry**: Verified ecosystem applications

### JavaScript SDK
- **`PaxeerWalletSDK.js`**: Complete integration library
- **Auto-detection**: Wallet providers and network switching
- **Event system**: Real-time connection status updates

### React Components
- **`PaxeerConnectButton.jsx`**: Drop-in React component
- **Customizable styling**: Multiple variants and themes

## 🚀 Quick Start

### 1. Deploy Wallet Manager

```bash
cd /root/syncron-labs-Contracts_Repo
npx hardhat run scripts/deploy-wallet-manager.js --network paxeer
```

### 2. Integrate in Your dApp

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://cdn.ethers.io/lib/ethers-5.7.2.umd.min.js"></script>
    <script src="path/to/PaxeerWalletSDK.js"></script>
</head>
<body>
    <script>
        // Initialize SDK
        const paxeerSDK = new PaxeerWalletSDK({
            dappId: 'your-dapp-id',
            dappName: 'Your dApp Name',
            autoConnect: true
        });

        // Handle connection events
        window.addEventListener('paxeer:connected', (event) => {
            console.log('Wallet connected:', event.detail.wallet);
        });

        window.addEventListener('paxeer:autoConnected', (event) => {
            console.log('Auto-connected:', event.detail.wallet);
        });
    </script>
</body>
</html>
```

### 3. React Integration

```jsx
import PaxeerConnectButton from './components/PaxeerConnectButton';

function App() {
    return (
        <PaxeerConnectButton
            dappId="your-dapp-id"
            dappName="Your dApp Name"
            onConnect={(data) => console.log('Connected:', data)}
            onDisconnect={() => console.log('Disconnected')}
        />
    );
}
```

## 🔧 Configuration

### SDK Configuration

```javascript
const paxeerSDK = new PaxeerWalletSDK({
    dappId: 'your-dapp-id',          // Required: Your dApp identifier
    dappName: 'Your dApp Name',       // Required: Display name
    domain: 'yourdapp.com',           // Optional: Domain for verification
    autoConnect: true,                // Optional: Enable auto-connect (default: true)
    sessionDuration: 24 * 60 * 60,   // Optional: Session duration in seconds
    walletManagerAddress: '0x...',    // Auto-loaded from config
});
```

### Session Management

```javascript
// Create session with custom duration
await paxeerSDK.createSession(7 * 24 * 60 * 60); // 7 days

// Check session status
const sessionInfo = await paxeerSDK.getSessionInfo();
console.log(sessionInfo);

// Extend session
await paxeerSDK.extendSession(24 * 60 * 60); // Add 24 hours

// Disconnect
await paxeerSDK.disconnect();
```

## 🎯 User Experience Flow

### First-Time User
1. User visits any Paxeer dApp
2. Clicks "Connect to Paxeer" button
3. Beautiful modal appears with wallet options
4. User selects wallet (MetaMask, WalletConnect, etc.)
5. Network automatically switches to Paxeer
6. Session created with signature verification
7. User is connected and can interact

### Returning User (Auto-Connect)
1. User visits any Paxeer dApp
2. SDK automatically detects existing session
3. **Zero-click connection** - instant access
4. User can immediately interact with dApp

### Cross-dApp Navigation
1. User connected to Paxeer DEX
2. Clicks link to Paxeer Lending
3. **Seamless transition** - no re-authentication
4. Same session works across all ecosystem dApps

## 🔐 Security Features

### Cryptographic Signatures
- Prevents session replay attacks
- Wallet ownership verification
- Nonce-based message signing

### Time-Based Sessions
- Configurable expiration times
- Automatic cleanup of expired sessions
- Manual session termination

### dApp Verification
- Only verified dApps can access user sessions
- Domain-based verification
- Admin controls for dApp registry

## 📊 Smart Contract API

### Core Functions

```solidity
// Create new session
function createSession(uint256 duration, bytes memory signature) external;

// Connect to dApp
function connectToDapp(string memory dappId, address wallet) external returns (bool);

// Check auto-connect eligibility
function canAutoConnect(address wallet, string memory dappId) external view returns (bool);

// Get session information
function getSessionInfo(address wallet) external view returns (
    uint256 sessionId,
    uint256 expiryTime,
    bool isActive,
    string[] memory connectedDapps
);

// Execute sponsored transaction
function executeTransaction(address target, bytes calldata data, string memory dappId) external;
```

### Admin Functions

```solidity
// Register new dApp
function registerDapp(string memory dappId, string memory name, string memory domain, address owner) external;

// Update session settings
function setSessionDuration(uint256 duration) external;
function setMaxSessionDuration(uint256 duration) external;

// dApp management
function deactivateDapp(string memory dappId) external;
function reactivateDapp(string memory dappId) external;
```

## 🎨 UI Customization

### Modal Styling
The SDK includes a beautiful, responsive modal that can be customized:

```javascript
// Custom modal styles
const paxeerSDK = new PaxeerWalletSDK({
    // ... config
    theme: {
        primary: '#667eea',
        secondary: '#764ba2',
        background: '#1a1a1a',
        text: '#ffffff'
    }
});
```

### React Component Props
```jsx
<PaxeerConnectButton
    variant="primary"        // primary, secondary, outline
    className="custom-class"
    size="large"            // small, medium, large
    showBalance={true}      // Display wallet balance
    showNetwork={true}      // Display network status
/>
```

## 🚦 Testing

### Local Testing
1. Start local Hardhat node
2. Deploy contracts with test data
3. Open example dApp in browser
4. Test connection flow

### Production Testing
1. Deploy to Paxeer testnet
2. Register test dApps
3. Verify cross-dApp navigation
4. Test session persistence

## 🌐 Ecosystem Integration

### Supported dApps
- **Paxeer DEX**: Token swapping and liquidity
- **Paxeer Lending**: Borrowing and lending
- **Paxeer NFTs**: NFT marketplace
- **Paxeer DAO**: Governance and voting
- **Paxeer Bridge**: Cross-chain transfers

### Adding New dApps
```javascript
// Register via smart contract
await walletManager.registerDapp(
    "new-dapp-id",
    "New dApp Name", 
    "newdapp.paxeer.network",
    ownerAddress
);
```

## 🔄 Migration Guide

### From Traditional Wallet Connectors
1. Remove existing wallet connection libraries
2. Install Paxeer SDK
3. Update connection logic
4. Test auto-connect functionality

### From Other SSO Solutions
1. Export user session data
2. Deploy Paxeer Wallet Manager
3. Migrate user accounts
4. Update all dApp integrations

## 🎉 Benefits

### For Users
- ✅ **One-click access** to entire ecosystem
- ✅ **Zero gas fees** for all transactions
- ✅ **Seamless experience** between dApps
- ✅ **Secure sessions** with cryptographic proof

### For Developers
- ✅ **Simple integration** with drop-in components
- ✅ **Consistent UX** across all dApps
- ✅ **No external dependencies** on wallet providers
- ✅ **Built-in session management**

### For the Ecosystem
- ✅ **Higher user retention** due to seamless UX
- ✅ **Increased cross-dApp usage**
- ✅ **Lower barrier to entry** for new users
- ✅ **Enhanced security** through verified dApps

## 🤝 Support

For questions, issues, or feature requests:
- Create an issue in the repository
- Join the Paxeer Discord community
- Check the documentation examples

---

**Built for the Paxeer ecosystem** 🚀
*Revolutionizing Web3 user experience through seamless connectivity*
