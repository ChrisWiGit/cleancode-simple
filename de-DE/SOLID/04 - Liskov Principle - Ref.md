# Liskov Substitution Principle (LSP)

Das Liskov Substitution Principle besagt, dass Objekte einer Superklasse durch Objekte einer Subklasse ersetzt werden können, ohne dass sich dadurch die Korrektheit des Programms ändert.


## Beispiel (Pascal)

### Beispiel

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
    function CanWithdraw(Amount: Double): Boolean; virtual;
  end;

  TSavingsAccount = class(TBankAccount)
  public
    function CanWithdraw(Amount: Double): Boolean; override;
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
  if CanWithdraw(Amount) then
    FBalance := FBalance - Amount
  else
    raise Exception.Create('Cannot withdraw the specified amount');
end;

function TBankAccount.GetBalance: Double;
begin
  Result := FBalance;
end;

function TBankAccount.CanWithdraw(Amount: Double): Boolean;
begin
  Result := Amount <= FBalance;
end;

{ TSavingsAccount }

function TSavingsAccount.CanWithdraw(Amount: Double): Boolean;
begin
  // Savings account doesn't allow withdrawals
  Result := False;
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
    if Account.CanWithdraw(200) then
      Account.Withdraw(200)
    else
      Writeln('Withdrawals not allowed from savings account');
    Writeln('Balance: ', Account.GetBalance:0:2);
  finally
    Account.Free;
  end;
end.


```