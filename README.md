# **Guide to Using Beacon Kit by Berachain**

## **Overview**

The `beacon-kit` is a toolset designed to facilitate the use of Ethereum Beacon Chain APIs. It simplifies interacting with the Ethereum consensus layer (Beacon Chain) and is aimed at developers building staking, validating, or other Ethereum Beacon-related services.

## **Prerequisites**

Before starting, ensure that you have the following installed:
- **Node.js** (v14.x or higher)
- **NPM** (v6.x or higher)
- Basic knowledge of JavaScript/TypeScript

## **Getting Started**

### **Step 1: Clone the Repository**

Start by cloning the `beacon-kit` repository from GitHub:

```bash
git clone https://github.com/berachain/beacon-kit.git
cd beacon-kit
```

### **Step 2: Install Dependencies**

Install the required Node.js dependencies by running:

```bash
npm install
```

This command will install all the necessary packages and dependencies for the `beacon-kit`.

### **Step 3: Basic Usage Example**

The `beacon-kit` provides several key functions for interacting with Ethereum's Beacon Chain. Below is a basic example of how to use the kit to query the Beacon Chain:

#### **Initialize and Fetch Beacon Chain Data**

1. **Create a Script (`index.js`)**:

Create a new file, `index.js`, and write the following code:

```js
const { BeaconAPI } = require('beacon-kit');

// Initialize BeaconAPI instance with a Beacon Chain node endpoint
const beaconAPI = new BeaconAPI({
  endpoint: 'https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID',
});

// Async function to fetch Beacon Chain data
const getBeaconChainData = async () => {
  try {
    // Fetch the current beacon state
    const state = await beaconAPI.getState();
    console.log('Beacon State:', state);

    // Fetch the current beacon chain head
    const head = await beaconAPI.getHead();
    console.log('Beacon Chain Head:', head);

    // Fetch validators
    const validators = await beaconAPI.getValidators();
    console.log('Validators:', validators);

  } catch (error) {
    console.error('Error fetching data from Beacon Chain:', error);
  }
};

// Call the function to fetch data
getBeaconChainData();
```

In this script:

- The `BeaconAPI` class is used to communicate with the Beacon Chain.
- Replace `'YOUR_INFURA_PROJECT_ID'` with your own Infura project ID or another Ethereum node endpoint.
- The script queries the current state, chain head, and validators on the Ethereum Beacon Chain.

### **Step 4: Run the Script**

After writing the script, run it using Node.js:

```bash
node index.js
```

You should see the output with information about the current beacon state, chain head, and validator list in the terminal.

---

## **Advanced Usage**

### **Fetching Validator Performance**

The `beacon-kit` also allows querying validator performance, which is useful for staking services:

```js
const getValidatorPerformance = async () => {
  try {
    const performance = await beaconAPI.getValidatorPerformance();
    console.log('Validator Performance:', performance);
  } catch (error) {
    console.error('Error fetching validator performance:', error);
  }
};

getValidatorPerformance();
```

### **Submitting a Transaction**

Here is an example of how to submit a transaction on the Beacon Chain:

```js
const submitTransaction = async () => {
  try {
    const transaction = {
      sender: '0xYourAddress',
      receiver: '0xReceiverAddress',
      amount: '1000000000', // Amount in Gwei
    };

    const result = await beaconAPI.sendTransaction(transaction);
    console.log('Transaction submitted:', result);
  } catch (error) {
    console.error('Error submitting transaction:', error);
  }
};

submitTransaction();
```

This is useful for validators or dApps that want to interact with the consensus layer directly.
