readme.md
# Efficient Data Storage & Compression Utilities

A sophisticated Aptos Move smart contract providing intelligent data compression and secure storage capabilities on the blockchain.

## 🚀 Features

### Intelligent Compression
- **Automatic Algorithm Selection**: Analyzes data patterns and chooses optimal compression method
- **Multiple Compression Types**: 
  - Run-Length Encoding (RLE) for repetitive data
  - Dictionary compression for pattern-based data
  - Pass-through for incompressible data
- **Efficiency Validation**: Only applies compression if it reduces data size

### Secure Storage
- **SHA3-256 Integrity Verification**: Every data chunk is protected with cryptographic checksums
- **Chunked Architecture**: Organizes data into manageable, indexed chunks
- **Automatic Corruption Detection**: Verifies data integrity on every retrieval

### Storage Analytics
- **Compression Metrics**: Tracks original vs compressed sizes
- **Storage Statistics**: Monitors total storage efficiency
- **Chunk Management**: Maintains metadata for each stored chunk

## 📋 Contract Structure

### Main Functions

#### `store_with_optimal_compression(account: &signer, data: vector<u8>)`
- Analyzes input data patterns
- Selects and applies optimal compression algorithm
- Stores compressed data with integrity checksums
- Updates storage statistics

#### `retrieve_and_decompress(account_addr: address, chunk_index: u64): vector<u8>`
- Retrieves data by chunk index
- Verifies data integrity using checksums
- Automatically decompresses based on stored compression type
- Returns original data

### Data Structures

```move
struct DataVault has key {
    chunks: vector<CompressedChunk>,
    total_original_size: u64,
    total_compressed_size: u64,
    chunk_count: u64,
}

struct CompressedChunk has store {
    data: vector<u8>,
    original_size: u64,
    compression_type: u8,
    checksum: vector<u8>,
}
```

## 🛠️ Usage Examples

### Basic Storage and Retrieval

```move
// Store data with automatic compression optimization
let sample_data = vector[1, 1, 1, 2, 2, 3, 3, 3, 3];
storage_addr::efficient_storage::store_with_optimal_compression(&signer, sample_data);

// Retrieve the first chunk (index 0)
let retrieved_data = storage_addr::efficient_storage::retrieve_and_decompress(
    signer::address_of(&signer), 
    0
);
```

### Multiple Data Chunks

```move
// Store multiple data chunks
storage_addr::efficient_storage::store_with_optimal_compression(&signer, dataset_1);
storage_addr::efficient_storage::store_with_optimal_compression(&signer, dataset_2);
storage_addr::efficient_storage::store_with_optimal_compression(&signer, dataset_3);

// Retrieve specific chunks
let chunk_0 = retrieve_and_decompress(address, 0);
let chunk_1 = retrieve_and_decompress(address, 1);
let chunk_2 = retrieve_and_decompress(address, 2);
```

## 🔧 Compression Algorithms

### Run-Length Encoding (RLE)
- **Best for**: Data with many consecutive repeated values
- **Example**: `[5,5,5,5,3,3,1] → [4,5,2,3,1,1]`
- **Compression Type**: 0

### Dictionary Compression
- **Best for**: Data with recurring patterns
- **Compression Type**: 1
- **Note**: Simplified implementation in current version

### Pass-Through (No Compression)
- **Used when**: Compression doesn't reduce data size
- **Compression Type**: 2

## ⚠️ Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| 1 | `E_VAULT_NOT_EXISTS` | DataVault resource doesn't exist for the account |
| 2 | `E_INVALID_CHUNK_ID` | Chunk index is out of bounds |
| 3 | `E_CHECKSUM_MISMATCH` | Data integrity verification failed |

## 🏗️ Deployment

1. **Compile the contract**:
   ```bash
   aptos move compile
   ```

2. **Deploy to network**:
   ```bash
   aptos move publish --named-addresses storage_addr=YOUR_ADDRESS
   ```

3. **Initialize storage** (automatically done on first use):
   - DataVault resource is created automatically when storing first chunk

## 📊 Performance Characteristics

- **Storage Efficiency**: 20-80% compression ratio for repetitive data
- **Integrity Protection**: SHA3-256 cryptographic verification
- **Gas Optimization**: Chunked architecture for efficient access
- **Scalability**: Supports multiple data chunks per account

## 🔒 Security Features

- **Data Integrity**: Cryptographic checksums prevent silent data corruption
- **Access Control**: Only account owner can store data
- **Public Verification**: Anyone can verify stored data integrity
- **Immutable Storage**: Stored chunks cannot be modified (only new chunks can be added)

## 🚧 Future Enhancements

- Advanced dictionary compression implementation
- Batch operations for multiple chunks
- Data deduplication across chunks
- Compression ratio analytics and reporting
- Time-based data expiration

## 📄 License

This smart contract is provided as-is for educational and development purposes.

## 🤝 Contributing

Feel free to suggest improvements or report issues. The contract is designed to be extensible for additional compression algorithms and storage features.
**contact details**
0x2786cde2d0d2bb0a212065b86317df680b9455a29d6efbab879db5b5b5701e26

![alt text](<../../Pictures/Screenshots/Screenshot 2025-08-07 145725.png>)