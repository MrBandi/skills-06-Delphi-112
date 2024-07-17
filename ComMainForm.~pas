unit ComMainForm;

interface

uses
  Windows, Messages, SysUtils, Classes, Graphics, Controls, Forms, Dialogs,
  StdCtrls, ExtCtrls, CPort, CPortCtl, ImgList ,jpeg , Registry, LPControl,
  SLControlCollection, LPControlDrawLayers, LPTransparentControl,
  ULBasicControl, ILLed ;

type
  TForm1 = class(TForm)
    ComPort: TComPort;
    Memo: TMemo;
    Button_Settings: TButton;
    Edit_Data: TEdit;
    Button_Send: TButton;
    NewLine_CB: TCheckBox;
    ComLed7: TComLed;
    Label1: TLabel;
    Label2: TLabel;
    Timer1: TTimer;
    Image1: TImage;
    Button1: TButton;
    ImageList1: TImageList;
    Button2: TButton;
    Button3: TButton;
    Image2: TImage;
    Image3: TImage;
    Image4: TImage;
    Image5: TImage;
    Image6: TImage;
    Image7: TImage;
    Image8: TImage;
    Button4: TButton;
    Image9: TImage;
    Button5: TButton;
    Edit1: TEdit;
    Label3: TLabel;
    Label4: TLabel;
    ComboBox1: TComboBox;
    Edit2: TEdit;
    Memo1: TMemo;
    GroupBox1: TGroupBox;
    ComboBox2: TComboBox;
    Button_Open: TButton;
    Button6: TButton;
    Label6: TLabel;
    Label7: TLabel;
    GroupBox2: TGroupBox;
    Edit3: TEdit;
    Edit4: TEdit;
    Button7: TButton;
    Button8: TButton;
    Edit5: TEdit;
    Label8: TLabel;
    Edit6: TEdit;
    Label9: TLabel;
    Edit7: TEdit;
    Label10: TLabel;
    Edit8: TEdit;
    Label11: TLabel;
    Edit9: TEdit;
    Label12: TLabel;
    Label13: TLabel;
    Edit10: TEdit;
    Button9: TButton;
    ComboBox3: TComboBox;
    Label14: TLabel;
    GroupBox3: TGroupBox;
    Label15: TLabel;
    GroupBox4: TGroupBox;
    GroupBox7: TGroupBox;
    GroupBox8: TGroupBox;
    Label5: TLabel;
    Label16: TLabel;
    Label17: TLabel;
    Edit11: TEdit;
    Edit12: TEdit;
    Edit13: TEdit;
    Button12: TButton;
    Memo2: TMemo;
    TimerYellow1: TTimer;
    TimerStrRx1: TTimer;
    TimerRed1: TTimer;
    TimerRGYLED: TTimer;
    DiceRed1: TILLed;
    DiceYellow1: TILLed;
    DiceGreen1: TILLed;
    DiceRed2: TILLed;
    DiceGreen2: TILLed;
    DiceYellow2: TILLed;
    DiceRed3: TILLed;
    procedure Button_OpenClick(Sender: TObject);
    procedure Button_SettingsClick(Sender: TObject);
    procedure Button_SendClick(Sender: TObject);
    procedure ComPortOpen(Sender: TObject);
    procedure ComPortClose(Sender: TObject);
    procedure ComPortRxChar(Sender: TObject; Count: Integer);
    procedure Timer1Timer(Sender: TObject);
    procedure Button1Click(Sender: TObject);
    procedure Button2Click(Sender: TObject);
    procedure Button3Click(Sender: TObject);
    procedure FormCreate(Sender: TObject);
    procedure Button4Click(Sender: TObject);
    procedure Button5Click(Sender: TObject);
    procedure ComboBox1Change(Sender: TObject);
    procedure ComboBox2DropDown(Sender: TObject);
    procedure ComboBox2Change(Sender: TObject);
    procedure Button6Click(Sender: TObject);
    procedure Button7Click(Sender: TObject);
    procedure Button8Click(Sender: TObject);
    procedure Button9Click(Sender: TObject);
    procedure ComboBox3Change(Sender: TObject);
    procedure Edit3KeyPress(Sender: TObject; var Key: Char);
    procedure Button12Click(Sender: TObject);
    procedure TimerStrRx1Timer(Sender: TObject);


  private
    { Private declarations }
  public
    { Public declarations }
      Led_index  : integer;
      tr: array[0..20] of TBaudRate;
      i : integer;
      WeekStr : String;
      textFormat : string;
      startLED: Boolean;
      stopLED: Boolean;
      Buffer: TStringList;
  end;

var
  Form1: TForm1;

implementation

{$R *.DFM}

procedure TForm1.Button_OpenClick(Sender: TObject);
var
  datetimeCome, str1: string;
begin
  ComPort.Open;
  Label7.Caption := 'Device Online';
  Label7.Color := clGreen;

  if ComPort.Connected then
  begin
     datetimeCome := FormatDateTime('yyyy,mm,dd,hh,mm,ss', Now);
     str1 := '{#04,' + datetimeCome + ';';
     ComPort.WriteStr(str1);
  end;
end;

procedure TForm1.Button6Click(Sender: TObject);
begin
      ComPort.Close;
      Label7.Caption := 'Device Offline';
      Label7.Color := clRed;
end;

procedure TForm1.Button_SettingsClick(Sender: TObject);
begin
  ComPort.ShowSetupDialog;
end;

procedure TForm1.Button_SendClick(Sender: TObject);
var
  Str: String;
begin
  Str := Edit_Data.Text;
  if NewLine_CB.Checked then
    Str := Str + #13#10;
  ComPort.WriteStr(Str);
end;

procedure TForm1.ComPortOpen(Sender: TObject);
begin
  //Button_Open.Caption := 'Open';
end;

procedure TForm1.ComPortClose(Sender: TObject);
begin
  //if Button_Open <> nil then
  //  Button_Open.Caption := 'Close';
end;

procedure TForm1.ComPortRxChar(Sender: TObject; Count: Integer);
var
  Str, CmdData: String;
  Black_bmp : Tbitmap;
  Green_bmp : Tbitmap;
  Red_bmp : Tbitmap;
  currentTime:TSystemTime;
  year, month, day, hour, minute, second, millisecond: string;
  datetime: string;
  x: integer;
begin
       Black_bmp := Tbitmap.Create;
       Green_bmp := Tbitmap.Create;
       Red_bmp := Tbitmap.Create;
       imagelist1.GetBitmap(0,Black_bmp);
       imagelist1.GetBitmap(1,Green_bmp);
       imagelist1.GetBitmap(2,Red_bmp);


       ComPort.ReadStr(Str, Count);
       Memo2.Lines.Add(Str);
       Buffer.Add(Str);
end;

procedure TForm1.Timer1Timer(Sender: TObject);
var
    currentTime:TSystemTime;
    year, month, day, hour, minute, second, millisecond: string;
    str, datetime: string;
begin

    GetSystemTime(currentTime);

    year:= IntToStr(currentTime.wYear);
    month:= IntToStr(currentTime.wMonth);
    day:= IntToStr(currentTime.wDay);
    hour:= IntToStr(currentTime.wHour + 8);
    minute:= IntToStr(currentTime.wMinute );
    second:= IntToStr(currentTime.wSecond);
    millisecond:= IntToStr(currentTime.wMilliseconds);

    //datetime:= year + '-' + month + '-' + day + '   ' + hour + ':' + minute + ':' + second + ':' + millisecond;
    //datetime:= FormatDateTime(Current Time:'yyyy-mm-dd hh:mm:ss', Now);
    datetime:= FormatDateTime('yyyy/mm/dd hh:mm:ss', Now);
    str := datetime;
    Label15.Caption := str;
end;

procedure TForm1.Button1Click(Sender: TObject);
var
     bmp : Tbitmap;

begin
       bmp := Tbitmap.Create;
       imagelist1.GetBitmap(0,bmp);

       image1.Picture.Assign(bmp);
end;

procedure TForm1.Button2Click(Sender: TObject);
var
     bmp : Tbitmap;
begin
       bmp := Tbitmap.Create;
       imagelist1.GetBitmap(1,bmp);

       image1.Picture.Assign(bmp);
end;

procedure TForm1.Button3Click(Sender: TObject);
var
     bmp : Tbitmap;
begin
       bmp := Tbitmap.Create;
       imagelist1.GetBitmap(2,bmp);

       image1.Picture.Assign(bmp);
end;

procedure TForm1.FormCreate(Sender: TObject);
var
     bmp : Tbitmap;
begin

       tr[0] := br110;
       tr[1] := br115200;
       tr[2] := br1200;
       tr[3] := br128000;
       tr[4] := br14400;
       tr[5] := br19200;
       tr[6] := br2400;
       tr[7] := br256000;
       tr[8] := br300;
       tr[9] := br38400;
       tr[10] := br4800;
       tr[11] := br56000;
       tr[12] := br57600;
       tr[13] := br600;
       tr[14] := br9600;
       tr[15] := brCustom;


       bmp := Tbitmap.Create;
       Led_index :=0;
       imagelist1.GetBitmap(Led_index,bmp);
       image2.Picture.Assign(bmp);
       image3.Picture.Assign(bmp);
       image4.Picture.Assign(bmp);
       image5.Picture.Assign(bmp);
       image6.Picture.Assign(bmp);
       image7.Picture.Assign(bmp);
       image8.Picture.Assign(bmp);
       image9.Picture.Assign(bmp);
       Label7.Caption := 'Device Offline';
       Label7.Color := clRed;
       startLED := False;
       stopLED := False;
       // 關閉所有的計時器
      TimerStrRx1.Enabled := true;
      Buffer := TStringList.Create;
      // 骰子1~3
      DiceRed1.Value := false;
      DiceYellow1.Value := false;
      DiceGreen1.Value := false;
      //骰子4
      DiceRed2.Value := false;
      //骰子5~7
      DiceGreen2.Value := false;
      DiceYellow2.Value := false;
      DiceRed3.Value := false;

end;

procedure TForm1.Button4Click(Sender: TObject);
var
     Black_bmp : Tbitmap;
     Green_bmp : Tbitmap;
     Red_bmp : Tbitmap;
begin
       Black_bmp := Tbitmap.Create;
       Green_bmp := Tbitmap.Create;
       Red_bmp := Tbitmap.Create;
       imagelist1.GetBitmap(0,Black_bmp);
       imagelist1.GetBitmap(1,Green_bmp);
       imagelist1.GetBitmap(2,Red_bmp);

       if (Led_index = 0) then
           begin
                 image2.Picture.Assign(Red_bmp);
                 image3.Picture.Assign(Black_bmp);
                 image4.Picture.Assign(Black_bmp);
                 image5.Picture.Assign(Black_bmp);
                 image6.Picture.Assign(Black_bmp);
                 image7.Picture.Assign(Black_bmp);
                 image8.Picture.Assign(Black_bmp);
                 image9.Picture.Assign(Black_bmp);
           end;

       if (Led_index = 1) then
           begin
                 image2.Picture.Assign(Black_bmp);
                 image3.Picture.Assign(Red_bmp);
                 image4.Picture.Assign(Black_bmp);
                 image5.Picture.Assign(Black_bmp);
                 image6.Picture.Assign(Black_bmp);
                 image7.Picture.Assign(Black_bmp);
                 image8.Picture.Assign(Black_bmp);
                 image9.Picture.Assign(Black_bmp);
           end;


       if (Led_index = 2) then
           begin
                 image2.Picture.Assign(Black_bmp);
                 image3.Picture.Assign(Black_bmp);
                 image4.Picture.Assign(Red_bmp);
                 image5.Picture.Assign(Black_bmp);
                 image6.Picture.Assign(Black_bmp);
                 image7.Picture.Assign(Black_bmp);
                 image8.Picture.Assign(Black_bmp);
                 image9.Picture.Assign(Black_bmp);
           end;

       if (Led_index = 3) then
           begin
                 image2.Picture.Assign(Black_bmp);
                 image3.Picture.Assign(Black_bmp);
                 image4.Picture.Assign(Black_bmp);
                 image5.Picture.Assign(Red_bmp);
                 image6.Picture.Assign(Black_bmp);
                 image7.Picture.Assign(Black_bmp);
                 image8.Picture.Assign(Black_bmp);
                 image9.Picture.Assign(Black_bmp);
           end;



       if (Led_index = 4) then
           begin
                 image2.Picture.Assign(Black_bmp);
                 image3.Picture.Assign(Black_bmp);
                 image4.Picture.Assign(Black_bmp);
                 image5.Picture.Assign(Black_bmp);
                 image6.Picture.Assign(Red_bmp);
                 image7.Picture.Assign(Black_bmp);
                 image8.Picture.Assign(Black_bmp);
                 image9.Picture.Assign(Black_bmp);
           end;

       if (Led_index = 5) then
           begin
                 image2.Picture.Assign(Black_bmp);
                 image3.Picture.Assign(Black_bmp);
                 image4.Picture.Assign(Black_bmp);
                 image5.Picture.Assign(Black_bmp);
                 image6.Picture.Assign(Black_bmp);
                 image7.Picture.Assign(Red_bmp);
                 image8.Picture.Assign(Black_bmp);
                 image9.Picture.Assign(Black_bmp);
           end;


       if (Led_index = 6) then
           begin
                 image2.Picture.Assign(Black_bmp);
                 image3.Picture.Assign(Black_bmp);
                 image4.Picture.Assign(Black_bmp);
                 image5.Picture.Assign(Black_bmp);
                 image6.Picture.Assign(Black_bmp);
                 image7.Picture.Assign(Black_bmp);
                 image8.Picture.Assign(Red_bmp);
                 image9.Picture.Assign(Black_bmp);
           end;

       if (Led_index = 7) then
           begin
                 image2.Picture.Assign(Black_bmp);
                 image3.Picture.Assign(Black_bmp);
                 image4.Picture.Assign(Black_bmp);
                 image5.Picture.Assign(Black_bmp);
                 image6.Picture.Assign(Black_bmp);
                 image7.Picture.Assign(Black_bmp);
                 image8.Picture.Assign(Black_bmp);
                 image9.Picture.Assign(Red_bmp);
           end;






       inc(Led_index);
       if  (Led_index >=8) then  Led_index:=0;


end;

procedure TForm1.Button5Click(Sender: TObject);
begin
      Memo.Clear;
end;

procedure TForm1.ComboBox1Change(Sender: TObject);
begin
       if (ComboBox1.ItemIndex >= 0) then
       begin
            ComPort.BaudRate := tr[ComboBox1.ItemIndex];
       end;
end;

procedure TForm1.ComboBox2DropDown(Sender: TObject);
var
  reg : TRegistry;
  sl: TStrings;
  i: integer;
begin
  Memo1.Clear;
  reg := TRegistry.Create;
  try
    reg.RootKey := HKEY_LOCAL_MACHINE;
    reg.Access := KEY_READ;
    reg.OpenKey('HARDWARE\DEVICEMAP\SERIALCOMM', false);
    sl := TStringList.Create;
    try
      reg.GetValueNames(sl);
      for i := 0 to sl.Count -1 do
        Memo1.Lines.Add(reg.ReadString(sl.Strings[i]));
    finally
      sl.Free;
    end;
  finally
    reg.CloseKey;
    reg.free;
  end;
  ComboBox2.Items.Assign(Memo1.Lines);

end;

procedure TForm1.ComboBox2Change(Sender: TObject);
begin
      ComPort.Port := ComboBox2.Text;
end;

procedure TForm1.Button7Click(Sender: TObject);
var
   Str: String;
   textStr : String;
begin
   textStr := Edit3.Text;
   textStr := Format('%4s', [textStr]);
   textStr := Trim(textStr);
   textFormat := Copy(textStr, 1, 2) + ',' + Copy(textStr, 3, 2);
   Str := '{#01,' + textFormat + ';';
   ComPort.WriteStr(Str);
end;

procedure TForm1.Button8Click(Sender: TObject);
var
   Str: String;
   StrLength : Integer;
begin
   Str := '{#02;';
   ComPort.WriteStr(Str);
end;

procedure TForm1.Button9Click(Sender: TObject);
var
     DateTimeStr : String;
begin

        DateTimeStr := '{#03,' + Edit5.Text + ',' + Edit6.Text + ',' + Edit7.Text + ',' + Edit8.Text + ',' + Edit9.Text + ',' + Edit10.Text + ';';
        ComPort.WriteStr(DateTimeStr);
end;

procedure TForm1.ComboBox3Change(Sender: TObject);
begin
         WeekStr :=  IntToStr(ComboBox3.ItemIndex);
end;

procedure TForm1.Edit3KeyPress(Sender: TObject; var Key: Char);
begin
  if not (Key in ['0'..'9', 'A'..'F', 'a'..'f', #8]) then
  begin
    Key := #0;
    ShowMessage('Not 4 Bits HEX Format');
  end
end;

procedure TForm1.Button12Click(Sender: TObject);
var
 alarmStr : String;
begin
    alarmStr := '{#05,' + Edit11.Text + ',' + Edit12.Text + ',' + Edit13.Text + ';';
    ComPort.WriteStr(alarmStr);
end;

procedure TForm1.TimerStrRx1Timer(Sender: TObject);
var
  Data, CmdData: String;
  x: Integer;
  ReceiveStr : TStringList;
begin
  while Buffer.Count > 0 do
  begin
    Data := Buffer[0];
    Buffer.Delete(0);
    ReceiveStr := TStringList.Create;
        try
          ReceiveStr.Delimiter := ',';           
          ReceiveStr.DelimitedText := Data;

          for x:=0 to (ReceiveStr.Count-1) do
          begin
            Data := ReceiveStr[x];

            if (Pos('}H', Data) = 1) or (Pos('H', Data) = 1) then
            begin
              if x < ReceiveStr.Count - 1 then
              begin
                CmdData := ReceiveStr[x + 1];
                Edit4.Text := CmdData;
              end;
            end;

            if (Pos('}L', Data) = 1) or (Pos('L', Data) = 1) then
            begin
              if x < ReceiveStr.Count - 1 then
              begin
                CmdData := ReceiveStr[x + 1];
                if (CmdData = '1') then
                begin
                  // 骰子1~3
                  DiceRed1.Value := false;
                  DiceYellow1.Value := false;
                  DiceGreen1.Value := false;
                  //骰子4
                  DiceRed2.Value := true;
                  //骰子5~7
                  DiceGreen2.Value := false;
                  DiceYellow2.Value := false;
                  DiceRed3.Value := false;
                end;
                if (CmdData = '2') then
                begin
                  // 骰子1~3
                  DiceRed1.Value := true;
                  DiceYellow1.Value := false;
                  DiceGreen1.Value := false;
                  //骰子4
                  DiceRed2.Value := false;
                  //骰子5~7
                  DiceGreen2.Value := false;
                  DiceYellow2.Value := false;
                  DiceRed3.Value := true;
                end;
                if (CmdData = '3') then
                begin
                  // 骰子1~3
                  DiceRed1.Value := true;
                  DiceYellow1.Value := false;
                  DiceGreen1.Value := false;
                  //骰子4
                  DiceRed2.Value := true;
                  //骰子5~7
                  DiceGreen2.Value := false;
                  DiceYellow2.Value := false;
                  DiceRed3.Value := true;
                end;
                if (CmdData = '4') then
                begin
                  // 骰子1~3
                  DiceRed1.Value := true;
                  DiceYellow1.Value := false;
                  DiceGreen1.Value := true;
                  //骰子4
                  DiceRed2.Value := false;
                  //骰子5~7
                  DiceGreen2.Value := true;
                  DiceYellow2.Value := false;
                  DiceRed3.Value := true;
                end;
                if (CmdData = '5') then
                begin
                  // 骰子1~3
                  DiceRed1.Value := true;
                  DiceYellow1.Value := false;
                  DiceGreen1.Value := true;
                  //骰子4
                  DiceRed2.Value := true;
                  //骰子5~7
                  DiceGreen2.Value := true;
                  DiceYellow2.Value := false;
                  DiceRed3.Value := true;
                end;
                if (CmdData = '6') then
                begin
                  // 骰子1~3
                  DiceRed1.Value := true;
                  DiceYellow1.Value := true;
                  DiceGreen1.Value := true;
                  //骰子4
                  DiceRed2.Value := false;
                  //骰子5~7
                  DiceGreen2.Value := true;
                  DiceYellow2.Value := true;
                  DiceRed3.Value := true;
                end;
              end;
            end;
          end;
          finally
            ReceiveStr.Free;
          end;
  end;
end;
end.




















