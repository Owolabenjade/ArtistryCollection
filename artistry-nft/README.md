# Artistry Collection 🎨

A comprehensive NFT smart contract built on Stacks blockchain using Clarity, featuring a built-in marketplace, royalty system, and secure minting capabilities.

## Overview

Artistry Collection is a feature-rich NFT implementation that goes beyond basic token functionality. It includes an integrated marketplace for trading, automatic royalty distribution to creators, and robust security features - all within a single, self-contained smart contract.

## Features

### 🖼️ NFT Core Functionality
- **Secure Minting**: Admin and public minting with custom metadata
- **Ownership Management**: Safe transfer mechanisms with validation
- **Metadata Storage**: On-chain storage of name, description, image, and creator info
- **Token URI Support**: Dynamic URI generation for metadata hosting

### 🏪 Built-in Marketplace
- **List for Sale**: Token owners can list NFTs at custom prices
- **Secure Purchasing**: Automated STX payment handling
- **Automatic Delisting**: Listings removed on transfer or sale
- **Market Discovery**: Query active listings and prices

### 💰 Creator Royalties
- **5% Creator Royalty**: Automatic distribution on secondary sales
- **Direct Payments**: STX transfers split between seller and original creator
- **Transparent**: All royalty calculations on-chain

### 🔒 Security Features
- **Input Validation**: Comprehensive checks on all user inputs
- **Authorization**: Owner-only functions and transfer permissions
- **Error Handling**: Meaningful error codes and safe failure modes
- **Anti-Manipulation**: Prevention of self-transfers and invalid operations

## Project Structure

```
artistry-nft/
├── contracts/
│   └── artistry.clar              # Main NFT smart contract
├── tests/
│   └── artistry_test.ts           # Test suite (to be added)
├── settings/
│   ├── Devnet.toml               # Development network config
│   ├── Testnet.toml              # Testnet configuration
│   └── Mainnet.toml              # Mainnet configuration
├── Clarinet.toml                 # Project configuration
├── README.md                     # This file
└── .gitignore                    # Git ignore patterns
```

## Getting Started

### Prerequisites
- [Clarinet](https://github.com/hirosystems/clarinet) - Stacks smart contract development tool
- [Node.js](https://nodejs.org/) (for testing)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/artistry-nft.git
   cd artistry-nft
   ```

2. **Install Clarinet** (if not already installed)
   ```bash
   # macOS
   brew install clarinet

   # Windows/Linux - Download from GitHub releases
   ```

3. **Check contract syntax**
   ```bash
   clarinet check
   ```

4. **Run tests** (when available)
   ```bash
   clarinet test
   ```

## Smart Contract Functions

### Read-Only Functions
- `get-last-token-id()` - Returns the latest minted token ID
- `get-token-uri(token-id)` - Returns metadata URI for a token
- `get-owner(token-id)` - Returns the owner of a specific token
- `get-token-metadata(token-id)` - Returns full metadata for a token
- `get-listing(token-id)` - Returns marketplace listing info

### Public Functions

#### Minting
- `mint-nft(name, description, image, recipient)` - Admin-only minting
- `public-mint()` - Public minting with STX payment

#### Trading
- `transfer(token-id, sender, recipient)` - Transfer NFT ownership
- `list-for-sale(token-id, price)` - List NFT on marketplace
- `buy-nft(token-id)` - Purchase listed NFT

#### Administration
- `set-mint-price(new-price)` - Update public mint price
- `set-base-uri(new-uri)` - Update metadata base URI

## Usage Examples

### Deploy Contract
```bash
clarinet deploy --devnet
```

### Mint an NFT (Admin)
```clarity
(contract-call? .artistry mint-nft 
    "Digital Masterpiece #1" 
    "A unique piece of digital art" 
    "https://ipfs.io/ipfs/..." 
    'ST1HTBVD3JG9C05J7HBJTHGR0GGW7KXW28M5JS8QE)
```

### List NFT for Sale
```clarity
(contract-call? .artistry list-for-sale u1 u5000000) ;; List token #1 for 5 STX
```

### Buy Listed NFT
```clarity
(contract-call? .artistry buy-nft u1) ;; Buy token #1
```

## Configuration

### Network Settings
The project includes configuration for all Stacks networks:
- **Devnet**: Local development
- **Testnet**: Public test network
- **Mainnet**: Production network

### Contract Variables
- **Mint Price**: 1 STX (1,000,000 microSTX)
- **Royalty Rate**: 5% of sale price
- **Base URI**: Configurable metadata endpoint

## Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| 100 | `err-owner-only` | Function restricted to contract owner |
| 101 | `err-not-token-owner` | Caller doesn't own the token |
| 102 | `err-listing-not-found` | No marketplace listing exists |
| 103 | `err-insufficient-funds` | Not enough STX for transaction |
| 104 | `err-token-not-found` | Token doesn't exist |
| 105 | `err-invalid-price` | Price must be greater than zero |
| 106 | `err-invalid-token-id` | Token ID must be greater than zero |
| 107 | `err-self-transfer` | Cannot transfer to same address |

## Testing

A comprehensive test suite is planned to cover:
- ✅ NFT minting and transfers
- ✅ Marketplace listing and purchasing
- ✅ Royalty distribution
- ✅ Access control and permissions
- ✅ Error handling scenarios
- ✅ Edge cases and security

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Security Considerations

- All user inputs are validated before processing
- Transfer functions include ownership verification
- Marketplace operations are atomic and safe
- No external dependencies to minimize attack surface
- Comprehensive error handling prevents unexpected states

## Roadmap

- [ ] Comprehensive test suite
- [ ] Web frontend interface
- [ ] Batch minting capabilities
- [ ] Advanced marketplace features (auctions, offers)
- [ ] IPFS integration for metadata
- [ ] Multi-collection support
