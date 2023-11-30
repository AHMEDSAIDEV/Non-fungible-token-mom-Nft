// Define starkhug token contract
contract StarkHugToken:
  // Define token balance mapping
  data balances : Map(Address, Uint256)
  
  // Define total supply
  data totalSupply : Uint256

  // Define token symbol
  data symbol : String

  // Event emitted when tokens are transferred
  event Transfer(from: Address, to: Address, amount: Uint256)

  // Initialize the token contract
  public function init():
    totalSupply := 100
    symbol := "L"
    balances[msg.sender] := totalSupply

  // Transfer tokens to another address
  public function transfer(to: Address, amount: Uint256):
    require(balances[msg.sender] >= amount, "Insufficient balance")
    balances[msg.sender] -= amount
    balances[to] += amount
    // Emit transfer event
    Transfer(from = msg.sender, to = to, amount = amount)

  // Get total supply of the token
  public function getTotalSupply() -> Uint256:
    return totalSupply

  // Get the token symbol
  public function getSymbol() -> String:
    return symbol

  // Get balance of a specific address
  public function getBalance(owner: Address) -> Uint256:
    return balances[owner]

