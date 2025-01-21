import hashlib
import time

def mine_block(previous_hash, data, difficulty):
    """
    Simulates mining a block by finding a hash below a difficulty threshold.
    """
    nonce = 0  # Start with nonce 0
    start_time = time.time()
    print(f"Starting mining with difficulty: {difficulty}")

    while True:
        # Create a string combining previous hash, data, and nonce
        text = previous_hash + data + str(nonce)
        
        # Compute SHA-256 hash
        hash_result = hashlib.sha256(text.encode()).hexdigest()
        
        # Check if the hash meets the difficulty requirement
        if hash_result.startswith('0' * difficulty):
            elapsed_time = time.time() - start_time
            print(f"Block mined! 🎉")
            print(f"Hash: {hash_result}")
            print(f"Nonce: {nonce}")
            print(f"Time taken: {elapsed_time:.2f} seconds")
            return hash_result, nonce

        # Increment nonce for the next attempt
        nonce += 1

def main():
    # Example previous hash (could be a hash of the previous block in the blockchain)
    previous_hash = "0000000000000000000abcdef123456789abcdef123456789abcdef1234567"
    
    # Example block data
    data = "Alice sends 1 BTC to Bob"
    
    # Mining difficulty (number of leading zeros required in the hash)
    difficulty = 4  # Higher difficulty = more computation
    
    # Start mining
    block_hash, nonce = mine_block(previous_hash, data, difficulty)
    print(f"New Block Hash: {block_hash}")
    print(f"Nonce used: {nonce}")

if __name__ == "__main__":
    main()
