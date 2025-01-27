# Ether.fi AVS Smart Contracts

Ether.fi utilizes a contract based AVS operator instead of an EOA in order to enable multiple security and efficiency improvements when working with a large number of eigenpods and AVS's

Each operator contract is a designed to be a simple forwarding contract

## Whitelisting an operation for an operator

    // specify which calls an node runner can make against which target contracts through the operator contract
    function updateAllowedOperatorCalls(uint256 _operatorId, address _target, bytes4 _selector, bool _allowed) external onlyAdmin {
        allowedOperatorCalls[_operatorId][_target][_selector] = _allowed;
        emit AllowedOperatorCallsUpdated(_operatorId, _target, _selector, _allowed);
    }

## Tracking operator actions
All forwarded operator actions will emit the following event

    event ForwardedOperatorCall(uint256 indexed id, address indexed target, bytes4 indexed selector, bytes data, address sender);

This can be used to track which actions have been taken by which operators

## General Overview

### Purpose and Functionality

The repository is named "Ether.fi AVS Smart Contracts" and it utilizes a contract-based AVS operator instead of an EOA to enable multiple security and efficiency improvements when working with a large number of eigenpods and AVS's.

### Main Contracts and Functionalities

- `src/AvsOperator.sol`: This contract defines the `AvsOperator` contract, which includes functions for initializing the contract, forwarding calls, registering as an operator, modifying operator details, updating metadata, and verifying signatures.
- `src/AvsOperatorManager.sol`: This contract defines the `AvsOperatorManager` contract, which manages the deployment and operation of `AvsOperator` contracts. It includes functions for registering operators, modifying operator details, forwarding calls, and managing operator actions.
- Various interface contracts in the `src/eigenlayer-interfaces` directory, such as `src/eigenlayer-interfaces/IAVSDirectory.sol`, `src/eigenlayer-interfaces/IBeaconChainOracle.sol`, and `src/eigenlayer-interfaces/IBLSApkRegistry.sol`, which define the interfaces for interacting with different components of the EigenLayer ecosystem.

### Configuration Files

The repository also includes configuration files such as `.gitignore`, `.gitmodules`, and `foundry.toml`, which are used for managing the development environment and dependencies.

### Continuous Integration

The repository uses GitHub Actions for continuous integration, as indicated by the presence of workflow files in the `.github/workflows` directory.
