# Open Closed Principle (OCP)

Das Open Closed Principle besagt, dass eine Klasse offen für Erweiterungen sein sollte, aber geschlossen für Modifikationen. 

Das bedeutet, dass eine Klasse durch Ableitung erweitert werden sollte, anstatt den bestehenden Code zu ändern.

## Beispiel (Pascal)

### Schlechtes Beispiel

```pascal
program OCPExample;

uses
  SysUtils;

type
  TMessageType = (mtEmail, mtSMS);

  TMessageProcessor = class
  public
    procedure ProcessMessage(MessageType: TMessageType; const Message: string);
  end;

procedure TMessageProcessor.ProcessMessage(MessageType: TMessageType; const Message: string);
begin
  case MessageType of
    mtEmail: Writeln('Processing Email: ', Message);
    mtSMS: Writeln('Processing SMS: ', Message);
  else
    Writeln('Unknown message type');
  end;
end;

var
  Processor: TMessageProcessor;
begin
  Processor := TMessageProcessor.Create;
  try
    Processor.ProcessMessage(mtEmail, 'Hello via Email');
    Processor.ProcessMessage(mtSMS, 'Hello via SMS');
  finally
    Processor.Free;
  end;
end.


```