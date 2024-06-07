# Liskov Substitution Principle (LSP)

Das Liskov Substitution Principle besagt, dass Objekte einer Superklasse durch Objekte einer Subklasse ersetzt werden können, ohne dass sich dadurch die Korrektheit des Programms ändert.


## Beispiel (Pascal)

### Schlechtes Beispiel

```pascal
program LSPExample;

{$MODE OBJFPC}

uses
  SysUtils;

type
  TBankAccount = class
  private
    FBalance: Double;
  public
    constructor Create(InitialBalance: Double);
    procedure Deposit(Amount: Double); virtual;
    procedure Withdraw(Amount: Double); virtual;
    function GetBalance: Double; virtual;
  end;

  TSavingsAccount = class(TBankAccount)
  public
    procedure Withdraw(Amount: Double); override;
  end;

{ TBankAccount }

constructor TBankAccount.Create(InitialBalance: Double);
begin
  FBalance := InitialBalance;
end;

procedure TBankAccount.Deposit(Amount: Double);
begin
  FBalance := FBalance + Amount;
end;

procedure TBankAccount.Withdraw(Amount: Double);
begin
  if Amount <= FBalance then
    FBalance := FBalance - Amount
  else
    raise Exception.Create('Insufficient funds');
end;

function TBankAccount.GetBalance: Double;
begin
  Result := FBalance;
end;

{ TSavingsAccount }

procedure TSavingsAccount.Withdraw(Amount: Double);
begin
  // hier wird gegen LSP verstoßen
  raise Exception.Create('Withdrawals not allowed from savings account');
end;

var
  Account: TBankAccount;
begin
  Account := TBankAccount.Create(1000);
  try
    Account.Deposit(500);
    Account.Withdraw(200);
    Writeln('Balance: ', Account.GetBalance:0:2);
  finally
    Account.Free;
  end;

  Account := TSavingsAccount.Create(1000);
  try
    Account.Deposit(500);
    // This will raise an exception, violating LSP
    Account.Withdraw(200);
    Writeln('Balance: ', Account.GetBalance:0:2);
  except
    on E: Exception do
      Writeln(E.Message);
  end;
end.


```