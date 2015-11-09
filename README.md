; Example of using ASin with degrees
#include <Math.au3>
#include <MsgBoxConstants.au3>
#include <WinAPI.au3>
#include <WindowsConstants.au3>

 Global $x
 Global $y
 Global $pos=MouseGetPos()
Global $PI = 3.141592653589793
Global $fDegToRad = $PI / 180

Func deseneaza($fcosy, $fsiny, $iLength, $iWidth, $iColor, $xt , $disty)
    Local $hDC, $hPen, $o_Orig

      $hDC = _WinAPI_GetWindowDC(0)
      $hPen = _WinAPI_CreatePen($PS_SOLID, $iWidth, $iColor)
      $o_Orig = _WinAPI_SelectObject($hDC, $hPen)

      _WinAPI_DrawLine($hDC, MouseGetPos()[0] , MouseGetPos()[1], MouseGetPos()[0]+138*$fcosy, MouseGetPos()[1]-138*$fsiny)

     ; clear resources
    _WinAPI_SelectObject($hDC, $o_Orig)
    _WinAPI_DeleteObject($hPen)
    _WinAPI_ReleaseDC(0, $hDC)

  $ok=MouseGetPos()
	  $ok[0]=$xt[0]


 $hDC = _WinAPI_GetWindowDC(0)
      $o_Orig = _WinAPI_SelectObject($hDC, $hPen)
    	  $hPen = _WinAPI_CreatePen($PS_SOLID, $iWidth, 0xFFFFFF)

	  While $ok[0]<$disty+$xt[0]
	  $ok[0]= $ok[0]+5
	  $o = $ok[0]-$xt[0]
	  $y=MouseGetPos()
	    _WinAPI_DrawLine($hDC,$ok[0] ,$y[1]-(($fsiny*$o/$fcosy)-(9.8*$o*$o/(2*10367.3435771*$fcosy*$fcosy))), $ok[0], $y[1]-(($fsiny*$o/$fcosy)-(9.8 * $o*$o/(2*10367.3435771*$fcosy*$fcosy)))-3)

	Wend

EndFunc   ;==>ShowCrosss()[0] & " " & MouseGetPos()[1])




Func deseneaza2($fcosy, $fsiny, $iLength, $iWidth, $iColor, $xt , $disty)
    Local $hDC, $hPen, $o_Orig

      $hDC = _WinAPI_GetWindowDC(0)
      $hPen = _WinAPI_CreatePen($PS_SOLID, $iWidth, $iColor)
      $o_Orig = _WinAPI_SelectObject($hDC, $hPen)

      _WinAPI_DrawLine($hDC, MouseGetPos()[0] , MouseGetPos()[1], MouseGetPos()[0]-138*$fcosy, MouseGetPos()[1]-138*$fsiny)

     ; clear resources
    _WinAPI_SelectObject($hDC, $o_Orig)
    _WinAPI_DeleteObject($hPen)
    _WinAPI_ReleaseDC(0, $hDC)

	  $ok=MouseGetPos()
	  $ok[0]=$xt[0]


 $hDC = _WinAPI_GetWindowDC(0)
      $o_Orig = _WinAPI_SelectObject($hDC, $hPen)
    	  $hPen = _WinAPI_CreatePen($PS_SOLID, $iWidth, 0xFFFFFF)

	  While $ok[0]>$xt[0]-$disty
	  $ok[0]= $ok[0]-5
	  $o = Abs($ok[0]-$xt[0])
	  $y=MouseGetPos()
	    _WinAPI_DrawLine($hDC,$ok[0] ,$y[1]-(($fsiny*$o/$fcosy)-(9.8*$o*$o/(2*10367.3435771*$fcosy*$fcosy))), $ok[0], $y[1]-(($fsiny*$o/$fcosy)-(9.8 * $o*$o/(2*10367.3435771*$fcosy*$fcosy)))-3)

	Wend

EndFunc




HotkeySet("{F4}",_punct1)

Func _punct1()
	  $y=0
	  $x=MouseGetPos()
	  $done = 0
	  HotkeySet("{F4}",_punct2)
    While $y=0
	  MouseMove(MouseGetPos()[0],$x[1])
    Wend
EndFunc
#include <WinAPI.au3>
#include <WindowsConstants.au3>

Func _punct2()

   $y=MouseGetPos()
   HotkeySet("{F4}",_punct1)
   $dist = $y[0] - $x[0]


   if $dist>0 then
   $fDegree = _Degree(ASin($dist*9.8/10367.3435771))
   $unghi=(180-$fDegree)/2
   $unghi2=$fDegree/2
$fcos =Abs(Cos($unghi*3.14159265/180))
$fsin =Abs(sin($unghi*3.14159265/180))
$fcos2 =Abs(Cos($unghi2*3.14159265/180))
$fsin2 =Abs(sin($unghi2*3.14159265/180))
MouseMove($x[0],$x[1])
deseneaza($fcos, $fsin, 20, 2, 0x0000FF, $x, $dist)
deseneaza($fcos2, $fsin2, 20, 2, 0x0000FF, $x, $dist)
   Local $raspuns=InputBox("Unde vrei sa lovesti?","1-unghiul de sus. 2-unghiul de jos")
   If $raspuns=1 then
	MouseMove(MouseGetPos()[0],MouseGetPos()[1]-138*$fsin,0)
	MouseMove(MouseGetPos()[0]+138*$fcos,MouseGetPos()[1],0)
	MouseClick("left")
 elseif $raspuns=2 Then
	MouseMove(MouseGetPos()[0],MouseGetPos()[1]-138*$fsin2,0)
	MouseMove(MouseGetPos()[0]+138*$fcos2,MouseGetPos()[1],0)
	MouseClick("left")

   EndIf


ElseIf $dist<0 then
   $dist=Abs($dist)
      $fDegree = _Degree(ASin($dist*9.8/10367.3435771))
   $unghi=360-((180-$fDegree)/2)
   $unghi2=360-($fDegree/2)
$fcos =Abs(Cos($unghi*3.14159265/180))
$fsin =Abs(sin($unghi*3.14159265/180))
$fcos2 =Abs(Cos($unghi2*3.14159265/180))
$fsin2 =Abs(sin($unghi2*3.14159265/180))
MouseMove($x[0],$x[1])
deseneaza2($fcos, $fsin, 20, 2, 0x0000FF, $x, $dist)
deseneaza2($fcos2, $fsin2, 20, 2, 0x0000FF, $x, $dist)
   Local $raspuns=InputBox("Unde vrei sa lovesti?","1-unghiul de sus. 2-unghiul de jos")
   If $raspuns=1 then
	MouseMove(MouseGetPos()[0],MouseGetPos()[1]-138*$fsin,0)
	MouseMove(MouseGetPos()[0]-138*$fcos,MouseGetPos()[1],0)
	MouseClick("left")
 elseif $raspuns=2 Then
	MouseMove(MouseGetPos()[0],MouseGetPos()[1]-138*$fsin2,0)
	MouseMove(MouseGetPos()[0]-138*$fcos2,MouseGetPos()[1],0)
	MouseClick("left")

   EndIf



   EndIf


EndFunc

While sleep(10000000)
   Wend


