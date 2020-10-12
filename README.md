// Project: Pong 
// Created: 2019-02-14
// Author: Jainilkumar Patel

// show all errors
SetErrorMode(2)

// set window properties
SetWindowTitle( "Pong" )
SetWindowSize( 1000, 750, 0 )
SetWindowAllowResize( 1 ) // allow the user to resize the window

// set display properties
SetVirtualResolution( 1000, 750 ) // doesn't have to match the window
SetOrientationAllowed( 1, 1, 1, 1 ) // allow both portrait and landscape on mobile devices
SetSyncRate( 30, 0 ) // 30fps instead of 60 to save battery
SetScissor( 0,0,0,0 ) // use the maximum available screen space, no black borders
UseNewDefaultFonts( 1 ) // since version 2.0.22 we can use nicer default fonts
// Some Info about some commands //

/* 
GetVirtualWidth() -- The Width size of the screen
GetVirtualHeight() -- The Height of the screen
GetSpriteHeight(#) -- The Hight of the sprite number
GetSpriteWidth(#) -- The Width of the sprite number
CreateText(#,"words") -- Creates a sprite but for words
str(Variable) -- Changes the variable to it's real value (usually used for text sprites)
*/

// INDEX //
/* 
Sprite info --- Line 80 to 118 
	Player 1 Sprite info --- Line 82 to 91
	Player 2 Sprite info --- Line 91 to 100
	Ball Sprite info --- Line 100 to 109
	Power up Sprite info --- Line 109 to 118

Text Sprite info --- Line 118 to 231
	Main Menu opening words --- Line 120 to 130
	Information on Main Menu --- Line 130 to 140
	Normal mode start screen opening words --- Line 140 to 146
	Informatin for Normal mode start screen --- Line 146 to 168
	Player 1 Score --- Line 168 to 175
	Player 2 Score --- Line 175 to 181
	Player 1 wins --- Line 181 to 186
	Player 2 wins --- Line 186 to 191
	Play again info --- Line 191 to 197
	Normal mode start screen opening words --- Line 197 to 203
	Informatin for Normal mode start screen --- Line 203 to 225
	Press ALT + F4 to end game --- Line 225 to 231
	
Variables --- Line 231 to 246

Order of code that is being run --- Line 251 to 262

All of the Subrountine --- Line 262 to 953
	Main Menu --- Line 264 to 296
	Pick Mode --- Line 296 to 314
	Endless mode --- Line 314 to 349
	Normal mode --- Line 349 to 384
	Start or go back Normal --- Line 384 to 400
	Start  or go back Endless --- Line 400 to 415
	Endless Game play --- Line 420 to 457
	Normal Game play --- Line 462 to 555
	Player 1 move --- Line 560 to 584
	Player 2 move --- Line 584 to 610
	Ball move --- Line 610 to 655
	Ball and Player Collision --- Line 655 to 670 
	Score --- Line 670 to 756
	Exit Game --- Line 756 to 766
	Ball Speed up --- Line 766 to 794
	Play Again --- Line 794 to 836
	Power up --- Line 854 to 953

*/
// End of Index //

/////\\\\\ Input information /////\\\\\ 
 
///\\\ Sprites ///\\\

//\\ Player 1 Sprite //\\
CreateImageColor(1, 255, 255, 255, 255) // Set Player 1 color as white //
CreateSprite(1, 1) // created sprite //
SetSpriteSize(1, 10, Player1_h) // Player 1 is 10 pixles wide and 125 pixles tall //
Player_1x = 10 
Player_1y = GetVirtualHeight() / 2 - GetSpriteHeight(1) / 2
SetSpritePosition(1, Player_1x, Player_1y) // Player 1 in the middle and most left side of the screen //


//\\ Player 2 Sprite //\\
CreateImageColor(2, 255, 255, 255, 255) // Set Player 2 color as white //
CreateSprite(2, 2) // created sprite //
SetSpriteSize(2, 10, Player2_h) // Player 1 is 10 pixles wide and 125 pixles tall //
Player_2x = GetVirtualWidth() - GetSpriteWidth(2) - 10
Player_2y = GetVirtualHeight() / 2 - GetSpriteHeight(2) / 2
SetSpritePosition(2, Player_2x, Player_2y) // Player 2 in the middle and most right side of the screen //


//\\ Ball Sprite //\\
CreateImageColor(3, 255, 255, 255, 255) // The color of the ball is white //
CreateSprite(3, 3) // created sprite //
SetSpriteSize(3, 15, 15) // The size of the ball is 15 pixles tall and 15 pixles wide //
Ball_x = GetVirtualWidth() / 2 - GetSpriteWidth(3) / 2
Ball_y = GetVirtualHeight() / 2 - GetSpriteHeight(3) / 2
SetSpritePosition(3, Ball_x, Ball_y) // The Ball will start in the center //


//\\ Power up //\\
CreateImageColor(4, 0, 252, 255, 255) // The color of the Power up is blue //
CreateSprite(4, 4) // created sprite //
SetSpriteSize(4, 50, 50) // The size of the ball is 50 pixles tall and 50 pixles wide //
Powerux = Random( 100, GetVirtualWidth() - 100)
Poweruy = Random( 100, GetVirtualHeight() - 100)
SetSpritePosition(4, Powerux, Poweruy) // The Ball will Randomly be place around 100 pixales away from all sides of the screen //


///\\\ Text Sprite ///\\\

//\\ Main Menu opening words //\\
CreateText(1,"Welcome to") 
CreateText(2, " Pong ")
SetTextColor(1, 255, 255, 255, 255) // Set color to white //
SetTextColor(2, 255, 255, 255, 255) // Set color to white //
SetTextSize(1, 100) // Set Size of text to 100 //
SetTextSize(2, 100) // Set Size of text to 100 //
SetTextPosition(1, GetVirtualWidth() / 2 - GetTextTotalWidth(1) / 2, GetVirtualHeight() / 2 - GetTextTotalHeight(1)) // Placed the text in the middle //
SetTextPosition(2, GetVirtualWidth() / 2 - GetTextTotalWidth(2) / 2, GetVirtualHeight() / 2) // Placed the text in the middle //

//\\ Information on Main Menu //\\
CreateText(3," Chose your mode:  Normal - (Press 1)   Endless - (Press 2) ") 
CreateText(4, " To exit press ALT and F4 ")
SetTextColor(3, 255, 255, 255, 100) // Set color to gray //
SetTextColor(4, 255, 255, 255, 100) // Set color to gray //
SetTextSize(3, 40) // Set Size of text to 40 //
SetTextSize(4, 40) // Set Size of text to 40 //
SetTextPosition(3, GetVirtualWidth() / 2 - GetTextTotalWidth(3) / 2, GetVirtualHeight() / 2 + GetTextTotalHeight(2)) // Placed the text under a text //
SetTextPosition(4, GetVirtualWidth() / 2 - GetTextTotalWidth(4) / 2, GetVirtualHeight() / 2 + GetTextTotalHeight(3) + GetTextTotalHeight(2)) // Placed the text under a text //

//\\ Normal mode start screen opening words //\\
CreateText(5, "Normal Mode")
SetTextColor(5, 255, 255, 255, 255) // Set color to white //
SetTextSize(5, 100) // Set Text Size to 100 //
SetTextPosition(5, GetVirtualWidth() / 2 - GetTextTotalWidth(5) / 2, GetVirtualHeight() / 2 - GetTextTotalHeight(5)) // Placed the text in the middle //

//\\ Informatin for Normal mode start screen //\\
CreateText(6, "Welcome to Normal mode! In this mode the first player to 10 points wins! Power Ups are")
CreateText(7, "blue squares and Power Downs are Red squares. Player 1 keys are W (up) and S (down).")
CreateText(8, "Player 2 keys are up and down keys. Get points by bouncing the ball pass your opponents")
CreateText(9, "paddle. Press ENTER to start game. Press BACKSPACE to go to Main Menu. Press ALT and")
CreateText(10, "F4 to end Game. Have Fun!")
SetTextColor(6, 255, 255, 255, 100) // Set color to gray //
SetTextSize(6, 30) // Set Size of text to 30 //
SetTextColor(7, 255, 255, 255, 100) // Set color to gray //
SetTextSize(7, 30) // Set Size of text to 30 //
SetTextColor(8, 255, 255, 255, 100) // Set color to gray //
SetTextSize(8, 30) // Set Size of text to 30 //
SetTextColor(9, 255, 255, 255, 100) // Set color to gray //
SetTextSize(9, 30) // Set Size of text to 30 //
SetTextColor(10, 255, 255, 255, 100) // Set color to gray //
SetTextSize(10, 30) // Set Size of text to 30 //
SetTextPosition(6, GetVirtualWidth() / 2 - GetTextTotalWidth(6) / 2, GetVirtualHeight() / 2 + GetTextTotalHeight(5)) // Placed the text under a text //
SetTextPosition(7, GetVirtualWidth() / 2 - GetTextTotalWidth(7) / 2, GetVirtualHeight() / 2 + GetTextTotalHeight(5) + GetTextTotalHeight(6)) // Placed the text under a text //
SetTextPosition(8,  GetVirtualWidth() / 2 - GetTextTotalWidth(8) / 2, GetVirtualHeight() / 2 + GetTextTotalHeight(5) + GetTextTotalHeight(6) + GetTextTotalHeight(7)) // Placed the text under a text //
SetTextPosition(9,  GetVirtualWidth() / 2 - GetTextTotalWidth(9) / 2, GetVirtualHeight() / 2 + GetTextTotalHeight(5) + GetTextTotalHeight(6) + GetTextTotalHeight(7) + GetTextTotalHeight(8))  // Placed the text under a text //
SetTextPosition(10,  GetVirtualWidth() / 2 - GetTextTotalWidth(10) / 2, GetVirtualHeight() / 2 + GetTextTotalHeight(5) + GetTextTotalHeight(6) + GetTextTotalHeight(7) + GetTextTotalHeight(8) + GetTextTotalHeight(9))  // Placed the text under a text //

// Player 1 Score //
Player1Score = 0
CreateText(11, str(Player1Score)) // Display player 1 score //
SetTextColor(11, 255, 255, 255, 255) // Set color to white //
SetTextSize(11, 100) // Set Size of text to 100 //
SetTextPosition(11, GetVirtualWidth() / 4 - GetTextTotalWidth(11)/2 , 10) // Played socre on the top left side //

// Player 2 Score //
CreateText(12, str(Player2Score)) // Display player 2 score //
SetTextColor(12, 255, 255, 255, 255)  // Set color to white // 
SetTextSize(12, 100) // Set Size of text to 100 //
SetTextPosition(12, (GetVirtualWidth() / 4) * 3 - GetTextTotalWidth(12)/2, 10) // Played socre on the top right side //

// Player 1 wins //
CreateText(13, "Player 1 Wins!!")
SetTextColor(13, 255, 255, 255, 255) // Set color to white //
SetTextSize(13, 100) // Set Size of text to 100 //
SetTextPosition(13, GetVirtualWidth() / 2 - GetTextTotalWidth(13) / 2 , GetVirtualHeight() / 2 - GetTextTotalHeight(13) / 2 ) // placed text in the middle //
// Player 2 wins //
CreateText(14, "Player 2 Wins!!")
SetTextColor(14, 255, 255, 255, 255) // Set color to white //
SetTextSize(14, 100) // Set Size of text to 100 //
SetTextPosition(14, GetVirtualWidth() / 2 - GetTextTotalWidth(14) / 2 , GetVirtualHeight() / 2 - GetTextTotalHeight(14) / 2) // placed text in the middle //
// Play again info //
CreateText(15, "Play Again? Yes - (Press Y) No - (Press N)")
SetTextColor(15, 255, 255, 255, 100) // Set color to gray //
SetTextSize(15, 30) // Set Size of text to 30 //
SetTextPosition(15, GetVirtualWidth() / 2 - GetTextTotalWidth(15) / 2, GetVirtualHeight() / 2 + GetTextTotalHeight(13)) // Placed the text under a text //

//\\ Normal mode start screen opening words //\\
CreateText(16, "Endless Mode")
SetTextColor(16, 255, 255, 255, 255)
SetTextSize(16, 100)
SetTextPosition(16, GetVirtualWidth() / 2 - GetTextTotalWidth(16) / 2, GetVirtualHeight() / 2 - GetTextTotalHeight(16)) // Placed the text in the middle //

//\\ Informatin for Normal mode start screen //\\
CreateText(17, "Welcome to Endless mode! In this mode the continus for ever! Power Ups are")
CreateText(18, "blue squares and Power Downs are Red squares. Player 1 keys are W (up) and S (down).")
CreateText(19, "Player 2 keys are up and down keys. Get points by bouncing the ball pass your")
CreateText(20, "opponents paddle. Press ENTER to start game. Press BACKSPACE to go to Main Menu. Press")
CreateText(21, "ALT and F4 to end Game. Have Fun!")
SetTextColor(17, 255, 255, 255, 100) // Set color to gray //
SetTextSize(17, 30) // Set Size of text to 30 //
SetTextColor(18, 255, 255, 255, 100) // Set color to gray //
SetTextSize(18, 30) // Set Size of text to 30 //
SetTextColor(19, 255, 255, 255, 100) // Set color to gray //
SetTextSize(19, 30) // Set Size of text to 30 //
SetTextColor(20, 255, 255, 255, 100) // Set color to gray //
SetTextSize(20, 30) // Set Size of text to 30 //
SetTextColor(21, 255, 255, 255, 100) // Set color to gray //
SetTextSize(21, 30) // Set Size of text to 30 //
SetTextPosition(17, GetVirtualWidth() / 2 - GetTextTotalWidth(17) / 2, GetVirtualHeight() / 2 + GetTextTotalHeight(16)) // Placed the text under a text //
SetTextPosition(18, GetVirtualWidth() / 2 - GetTextTotalWidth(18) / 2, GetVirtualHeight() / 2 + GetTextTotalHeight(16) + GetTextTotalHeight(17)) // Placed the text under a text //
SetTextPosition(19, GetVirtualWidth() / 2 - GetTextTotalWidth(19) / 2, GetVirtualHeight() / 2 + GetTextTotalHeight(16) + GetTextTotalHeight(17) + GetTextTotalHeight(18)) // Placed the text under a text //
SetTextPosition(20, GetVirtualWidth() / 2 - GetTextTotalWidth(20) / 2, GetVirtualHeight() / 2 + GetTextTotalHeight(16) + GetTextTotalHeight(17) + GetTextTotalHeight(18) + GetTextTotalHeight(19))  // Placed the text under a text //
SetTextPosition(21, GetVirtualWidth() / 2 - GetTextTotalWidth(21) / 2, GetVirtualHeight() / 2 + GetTextTotalHeight(16) + GetTextTotalHeight(17) + GetTextTotalHeight(18) + GetTextTotalHeight(19) + GetTextTotalHeight(20)) // Placed the text under a text //

//\\ Press ALT + F4 to end game //\\
CreateText(22, "Press ALT + F4 to End Game")
SetTextColor(22, 255, 255, 255, 255)
SetTextSize(22, 15)
SetTextPosition(22, 0 ,0)

///\\\ Variables ///\\\
Player1Score = 0 // Variable for the player 1 score //
Player2Score = 0 // Variable for the player 1 score //
Player1_h = 125 // Variable for the player 1 paddle height //
Player2_h = 125 // Variable for the player 1 paddle height //
start = 1 // Variable used to decide which mode to select //
Game_Play = 0  // Variable used to decide which game mode to start //
DRIX = Random (0, 1) // Ball X movement is random (1 - move left) (0 - move right) // 
DRIY = Random (0, 1) // Ball Y movement is random (1 - move down) (0 - move up) // 
BallSpeed = 10 // starting speed of ball // 
Playerspeed = 15 // starting player speed //
count = 1
Powergiven = 0
Powergiven1 = 0
Powergiven2 = 0

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
////\\\\ REAL CODE START HERE ////\\\\                                                                                                                       //
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

// Order of code that is being run //
do
    gosub Main_menu // Main Menu Start Screen //
    gosub Normal_mode // Normal Mode Start Screen //
    gosub Normal_Game_play // Normal Mode Game //
    gosub Endless_mode // Endless Mode Start Screen //
    gosub Endless_Game_play // Endless Mode Game //
    Sync()
loop


/////\\\\\ All of the Subrountine /////\\\\\

//\\ Main Menu //\\
Main_menu: // Main Menu Start Screen //
While start = 1
	SetSpriteVisible(1, 0) // Player 1 paddle is hiddin //
	SetSpriteVisible(2, 0) // Player 2 paddle is hiddin //
	SetSpriteVisible(3, 0) // Ball is hiddin //
	SetSpriteVisible(4, 0) // Power up is hiddin //
	SetTextVisible(1, 1) // Main Menu Info is shown //
	SetTextVisible(2, 1) // Main Menu Info is shown //
	SetTextVisible(3, 1) // Main Menu Info is shown //
	SetTextVisible(4, 1) // Main Menu Info is shown //
	SetTextVisible(5, 0) // Normal Mode info is not shown //
	SetTextVisible(6, 0) // Normal Mode info is not shown //
	SetTextVisible(7, 0) // Normal Mode info is not shown //
	SetTextVisible(8, 0) // Normal Mode info is not shown //
	SetTextVisible(9, 0) // Normal Mode info is not shown //
	SetTextVisible(10, 0) // Normal Mode info is not shown //
	SetTextVisible(13, 0) // Player 1 Win Text is not shown //
	SetTextVisible(14, 0) // Player 2 Win Text is not shown //
	SetTextVisible(15, 0) // Play Again Text is not shown //
	SetTextVisible(16, 0) // Endless mode info is not shown //
	SetTextVisible(17, 0) // Endless mode info is not shown //
	SetTextVisible(18, 0) // Endless mode info is not shown //
	SetTextVisible(19, 0) // Endless mode info is not shown //
	SetTextVisible(20, 0) // Endless mode info is not shown //
	SetTextVisible(21, 0) // Endless mode info is not shown //
	gosub Pick_Mode
	gosub Exit_Game
	sync()
endwhile
return

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Pick_Mode:
if GetRawKeyState(49) = 1 // 49 is the number 1 key
	start = 2 // changes to the normal mode start screen
else 
	if GetRawKeyState(50) = 1 // 50 is the number 2 key
		start = 3 // changes to the endless mode start screen
	else 
		if GetRawKeyState(18) = 1 and GetRawKeyState(115) = 1 // 18 is the ALT key and 155 is the F4 key
			end // stops and end the game
		else
			start = 1 // keeps at the main menu screen
		endif
	endif
endif
return

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

//\\ Endless Start Screen //\\
Endless_mode:
While start = 3
// Intructions and text shown on the screen //
	SetSpriteVisible(1, 0) // Player 1 paddle is hiddin //
	SetSpriteVisible(2, 0) // Player 2 paddle is hiddin //
	SetSpriteVisible(3, 0) // Ball is hiddin //
	SetSpriteVisible(4, 0) // Power up is hiddin //
	SetTextVisible(1, 0) // Main Menu Info is not shown //
	SetTextVisible(2, 0) // Main Menu Info is not shown //
	SetTextVisible(3, 0) // Main Menu Info is not shown //
	SetTextVisible(4, 0) // Main Menu Info is not shown //
	SetTextVisible(5, 0) // Normal Mode info is not shown //
	SetTextVisible(6, 0) // Normal Mode info is not shown //
	SetTextVisible(7, 0) // Normal Mode info is not shown //
	SetTextVisible(8, 0) // Normal Mode info is not shown //
	SetTextVisible(9, 0) // Normal Mode info is not shown //
	SetTextVisible(10, 0) // Normal Mode info is not shown //
	SetTextVisible(13, 0) // Player 1 Win Text is not shown //
	SetTextVisible(14, 0) // Player 2 Win Text is not shown //
	SetTextVisible(15, 0) // Play Again Text is not shown //
	SetTextVisible(16, 1) // Endless mode info is shown //
	SetTextVisible(17, 1) // Endless mode info is shown //
	SetTextVisible(18, 1) // Endless mode info is shown //
	SetTextVisible(19, 1) // Endless mode info is shown //
	SetTextVisible(20, 1) // Endless mode info is shown //
	SetTextVisible(21, 1) // Endless mode info is shown //
	gosub Exit_Game 
	gosub Start_or_go_back_Endless
	sync()
endwhile
return

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

//\\ Normal Start Screen //\\
Normal_mode:
While start = 2
	// Intructions and text shown on the screen //
	SetSpriteVisible(1, 0) // Player 1 paddle is hiddin //
	SetSpriteVisible(2, 0) // Player 2 paddle is hiddin // 
	SetSpriteVisible(3, 0) // Ball is hiddin //
	SetSpriteVisible(4, 0) // Power up is hiddin //
	SetTextVisible(1, 0) // Main Menu Info is not shown //
	SetTextVisible(2, 0) // Main Menu Info is not shown //
	SetTextVisible(3, 0) // Main Menu Info is not shown //
	SetTextVisible(4, 0) // Main Menu Info is not shown //
	SetTextVisible(5, 1) // Normal Mode info is shown //
	SetTextVisible(6, 1) // Normal Mode info is shown //
	SetTextVisible(7, 1) // Normal Mode info is shown //
	SetTextVisible(8, 1) // Normal Mode info is shown //
	SetTextVisible(9, 1) // Normal Mode info is shown //
	SetTextVisible(10, 1) // Normal Mode info is shown //
	SetTextVisible(13, 0) // Player 1 Win Text is not shown //
	SetTextVisible(14, 0) // Player 2 Win Text is not shown //
	SetTextVisible(15, 0) // Play Again Text is not shown //
	SetTextVisible(16, 0) // Endless mode info is not shown //
	SetTextVisible(17, 0) // Endless mode info is not shown //
	SetTextVisible(18, 0) // Endless mode info is not shown //
	SetTextVisible(19, 0) // Endless mode info is not shown //
	SetTextVisible(20, 0) // Endless mode info is not shown //
	SetTextVisible(21, 0) // Endless mode info is not shown //
	gosub Exit_Game
	gosub Start_or_go_back_Normal
	sync()
endwhile
return

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Start_or_go_back_Normal:
if GetRawKeyState (8) = 1 // 8 is the Backspace key 
	start = 1 // changes to main menu
else
	if GetRawKeyState (13) = 1 // 13 is the Enter key
		Game_Play = 1 // start the Normal game play
		start = 0 // hid the info
	else
		start = start // the info shown stays
		Game_Play = Game_Play // the gameplay mode stays the same
	endif
endif
return

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Start_or_go_back_Endless:
if GetRawKeyState (8) = 1 // 8 is the Backspace key 
	start = 1 // changes to main menu
else
	if GetRawKeyState (13) = 1 // 13 is the Enter key
		Game_Play = 2 // start the Endless game play
		start = 0 // hid the info
	else
		start = start // the info shown stays
		Game_Play = Game_Play // the gameplay mode stays the same
	endif
endif
return

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
// Endless Mode                                                                                                                                                                                                //
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Endless_Game_play:
// game play info
while Game_Play = 2 
	SetSpriteVisible(1, 1) // Player 1 paddle is shown //
	SetSpriteVisible(2, 1) // Player 2 paddle is shown // 
	SetSpriteVisible(3, 1) // Ball is shown //
	SetSpriteVisible(4, 0) // Power up is hiddin //
	SetTextVisible(1, 0) // Main Menu Info is not shown //
	SetTextVisible(2, 0) // Main Menu Info is not shown //
	SetTextVisible(3, 0) // Main Menu Info is not shown //
	SetTextVisible(4, 0) // Main Menu Info is not shown //
	SetTextVisible(5, 0) // Normal Mode info is not shown //
	SetTextVisible(6, 0) // Normal Mode info is not shown //
	SetTextVisible(7, 0) // Normal Mode info is not shown //
	SetTextVisible(8, 0) // Normal Mode info is not shown //
	SetTextVisible(9, 0) // Normal Mode info is not shown //
	SetTextVisible(10, 0) // Normal Mode info is not shown //
	SetTextVisible(13, 0) // Player 1 Win Text is not shown //
	SetTextVisible(14, 0) // Player 2 Win Text is not shown //
	SetTextVisible(15, 0) // Play Again Text is not shown //
	SetTextVisible(16, 0) // Endless mode info is not shown //
	SetTextVisible(17, 0) // Endless mode info is not shown //
	SetTextVisible(18, 0) // Endless mode info is not shown //
	SetTextVisible(19, 0) // Endless mode info is not shown //
	SetTextVisible(20, 0) // Endless mode info is not shown //
	SetTextVisible(21, 0) // Endless mode info is not shown //
	gosub Player_1_move // Player 1 movement code //
	gosub Player_2_move // Player 2 movment code //
	gosub Ball_move // ball movement code //
	gosub Ball_Speed_up // ball speeding up code //
	gosub Ball_and_Player_Collision // ball boucing off of the paddles code //
	gosub Power_up // Power up code //
	gosub Score // score counting code //
	gosub Exit_Game // exiting game code //
	sync()
endwhile
return

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
// All code for Normal mode                                                                                                                                                                                   //
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Normal_Game_play:

while Game_Play = 1 
	if Player1Score > 9 // if player 1 gets 10 points
		SetSpriteVisible(1, 1) // Player 1 paddle is shown //
		SetSpriteVisible(2, 1) // Player 2 paddle is shown // 
		SetSpriteVisible(3, 0) // Ball is shown //
		SetSpriteVisible(4, 0) // Power up is hiddin //
		SetTextVisible(1, 0) // Main Menu Info is not shown //
		SetTextVisible(2, 0) // Main Menu Info is not shown //
		SetTextVisible(3, 0) // Main Menu Info is not shown //
		SetTextVisible(4, 0) // Main Menu Info is not shown //
		SetTextVisible(5, 0) // Normal Mode info is not shown //
		SetTextVisible(6, 0) // Normal Mode info is not shown //
		SetTextVisible(7, 0) // Normal Mode info is not shown //
		SetTextVisible(8, 0) // Normal Mode info is not shown //
		SetTextVisible(9, 0) // Normal Mode info is not shown //
		SetTextVisible(10, 0) // Normal Mode info is not shown //
		SetTextVisible(13, 1) // Player 1 Win Text is shown //
		SetTextVisible(14, 0) // Player 2 Win Text is not shown //
		SetTextVisible(15, 1) // Play Again Text is shown //
		SetTextVisible(16, 0) // Endless mode info is not shown //
		SetTextVisible(17, 0) // Endless mode info is not shown //
		SetTextVisible(18, 0) // Endless mode info is not shown //
		SetTextVisible(19, 0) // Endless mode info is not shown //
		SetTextVisible(20, 0) // Endless mode info is not shown //
		SetTextVisible(21, 0) // Endless mode info is not shown //
		gosub Play_Again // Play agian screen //
		gosub Exit_Game // exiting game code //
	else
		if Player2Score > 9
		SetSpriteVisible(1, 1) // Player 1 paddle is shown //
		SetSpriteVisible(2, 1) // Player 2 paddle is shown // 
		SetSpriteVisible(3, 0) // Ball is shown //
		SetSpriteVisible(4, 0) // Power up is hiddin //
		SetTextVisible(1, 0) // Main Menu Info is not shown //
		SetTextVisible(2, 0) // Main Menu Info is not shown //
		SetTextVisible(3, 0) // Main Menu Info is not shown //
		SetTextVisible(4, 0) // Main Menu Info is not shown //
		SetTextVisible(5, 0) // Normal Mode info is not shown //
		SetTextVisible(6, 0) // Normal Mode info is not shown //
		SetTextVisible(7, 0) // Normal Mode info is not shown //
		SetTextVisible(8, 0) // Normal Mode info is not shown //
		SetTextVisible(9, 0) // Normal Mode info is not shown //
		SetTextVisible(10, 0) // Normal Mode info is not shown //
		SetTextVisible(13, 0) // Player 1 Win Text is shown //
		SetTextVisible(14, 1) // Player 2 Win Text is not shown //
		SetTextVisible(15, 1) // Play Again Text is shown //
		SetTextVisible(16, 0) // Endless mode info is not shown //
		SetTextVisible(17, 0) // Endless mode info is not shown //
		SetTextVisible(18, 0) // Endless mode info is not shown //
		SetTextVisible(19, 0) // Endless mode info is not shown //
		SetTextVisible(20, 0) // Endless mode info is not shown //
		SetTextVisible(21, 0) // Endless mode info is not shown //
		gosub Play_Again // Play agian screen //
		gosub Exit_Game // exiting game code //
		else
			SetSpriteVisible(1, 1) // Player 1 paddle is shown //
			SetSpriteVisible(2, 1) // Player 2 paddle is shown // 
			SetSpriteVisible(3, 1) // Ball is shown //
			SetSpriteVisible(4, 0) // Power up is hiddin //
			SetTextVisible(1, 0) // Main Menu Info is not shown //
			SetTextVisible(2, 0) // Main Menu Info is not shown //
			SetTextVisible(3, 0) // Main Menu Info is not shown //
			SetTextVisible(4, 0) // Main Menu Info is not shown //
			SetTextVisible(5, 0) // Normal Mode info is not shown //
			SetTextVisible(6, 0) // Normal Mode info is not shown //
			SetTextVisible(7, 0) // Normal Mode info is not shown //
			SetTextVisible(8, 0) // Normal Mode info is not shown //
			SetTextVisible(9, 0) // Normal Mode info is not shown //
			SetTextVisible(10, 0) // Normal Mode info is not shown //
			SetTextVisible(13, 0) // Player 1 Win Text is not shown //
			SetTextVisible(14, 0) // Player 2 Win Text is not shown //
			SetTextVisible(15, 0) // Play Again Text is not shown //
			SetTextVisible(16, 0) // Endless mode info is not shown //
			SetTextVisible(17, 0) // Endless mode info is not shown //
			SetTextVisible(18, 0) // Endless mode info is not shown //
			SetTextVisible(19, 0) // Endless mode info is not shown //
			SetTextVisible(20, 0) // Endless mode info is not shown //
			SetTextVisible(21, 0) // Endless mode info is not shown //
			gosub Player_1_move // Player 1 movement code //
			gosub Player_2_move // Player 2 movment code //
			gosub Ball_move // ball movement code //
			gosub Ball_Speed_up // ball speeding up code //
			gosub Ball_and_Player_Collision // ball boucing off of the paddles code //
			gosub Power_up // Power up code //
			gosub Score // score counting code //
			gosub Exit_Game // exiting game code //
		endif
	endif
	sync()
endwhile
return

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
// All Subrountine for both Game Play                                                                                                                                                                         //
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Player_1_move:
if GetRawKeyState(87) = 1 // 87 is the W key 
	Player_1y = Player_1y - Playerspeed // moves the player 1 up
else
	if GetRawKeyState(83) = 1 // 83 is the S key
		Player_1y = Player_1y + Playerspeed // moves the player 1 down
	else
		Player_1y = Player_1y // otherwise the player stays at the same spot
	endif
endif

// boundaries for player 1 //
if Player_1y > GetVirtualHeight() - GetSpriteHeight(1) // if player 1 touches the edge of the bottom screen
	Player_1y = GetVirtualHeight() - GetSpriteHeight(1) // it stops
else
	if Player_1y < 0 // if player 1 touches the edge of the top screen
		Player_1y = 0 // it stops
	else
		Player_1y = Player_1y // otherwise it's position do not change
	endif
endif
SetSpritePosition(1, Player_1x, Player_1y)
return

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Player_2_move:
if GetRawKeyState(38) = 1 // 38 is the up key
	Player_2y = Player_2y - Playerspeed // moves the player 2 up
else
	if GetRawKeyState(40) = 1 // 40 is the down key
		Player_2y = Player_2y + Playerspeed // moves the player 2 down
	else
		Player_2y = Player_2y // otherwise the player stays at the same spot
	endif
endif

// boundaries for player 2 //
if Player_2y > GetVirtualHeight() - GetSpriteHeight(2) // if player 2 touches the edge of the bottom screen
	Player_2y = GetVirtualHeight() - GetSpriteHeight(2) // it stops
else
	if Player_2y < 0// if player 2 touches the edge of the top screen
		Player_2y = 0 // it stops
	else
		Player_2y = Player_2y // otherwise it's position do not change
	endif
endif
SetSpritePosition(2, Player_2x, Player_2y)
return

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Ball_move:
// Side way direction //
/* since I randomised the direction of DRIX to get
	a random starting direction i made it so that the
	direction for 1 is right and 0 is left */
if DRIX = 0
	DRIX = -1
else
	DRIX = DRIX
endif
Ball_x = Ball_x + DRIX*BallSpeed // the movement formula of the ball 
/* DRIX is the direction that the ball is traveling
	BallSpeed it the speed of the ball
*/

// Horizontal direction of the ball //
/* since I randomised the direction of DRIY to get
	a random starting direction I made it so that the
	direction for 1 is down and 0 is up */
if DRIY = 0
	DRIY = -1
else
	Ball_y = Ball_y
endif

// Vertical boundaries //
if Ball_y > GetVirtualHeight() - GetSpriteHeight(3) // if the ball touches the bottom of the screen it bounces up 
	DRIY = DRIY * -1 
else 
	if Ball_y < 0 // if the ball touches the top of the screen it bounces down
		DRIY = DRIY * -1
	else
		DRIY = DRIY // otherwise the direction stays the same
	endif
endif

Ball_y = Ball_y + DRIY*BallSpeed // the movement formula of the ball 
/* DRIY is the direction that the ball is traveling
	BallSpeed it the speed of the ball
*/
SetSpritePosition(3, Ball_x, Ball_y)
return

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Ball_and_Player_Collision:
if GetSpriteCollision(3, 1) = 1 // if the ball bounces player 1 paddle, it bounces away from it
	DRIX = DRIX * -1
else
	if GetSpriteCollision(3, 2) = 1 // if the ball bounces player 2 paddle, it bounces away from it
		DRIX = DRIX*-1
	else
		DRIX = DRIX // otherwise the direction of the ball stays the same
	endif
endif
SetSpritePosition(3, Ball_x, Ball_y)
return

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Score:

if Ball_x < 0 - 10 // if the ball gose past player 1
	
	// the ball is repositioned to the middle of the screen
	Ball_x = GetVirtualWidth()/2 - GetSpriteWidth(3)/2 
	Ball_y = GetVirtualHeight()/2 - GetSpriteHeight(3)/2
	Player2Score = Player2Score + 1 // player 2 gets a point
	
	// the starting direction of the ball is randomized
	DRIX = Random (0, 1) 
	DRIY = Random (0, 1)
	
	// player 2 score is displayed
	SetTextString(12, str(Player2Score))

	BallSpeed = 10 // the ball speed is reset
	Playerspeed = 10 // the players speeds are reset
	Powergiven = 0 // no power up has be given 
	Powergiven1 = 0 // player 1 dose not have power up 
	Powergiven2 = 0 // player 2 dose not have power up 
	ResetTimer() // resets the timer use to display the power up 
	SetSpriteVisible(4, 0) // power up is invisible
	
	// Players paddles are the same 
	Player1_h = 125
	Player2_h = 125
	
	// both playes is repotioned in the middle for both sides 
	Player_1y = GetVirtualHeight() / 2 - GetSpriteHeight(1) / 2
	Player_2y = GetVirtualHeight() / 2 - GetSpriteHeight(2) / 2
	
else
	if Ball_x > GetVirtualWidth() + 10 // if the ball goes past player 2
		
		// the ball is repositioned to the middle of the screen
		Ball_x = GetVirtualWidth()/2 - GetSpriteWidth(3)/2
		Ball_y = GetVirtualHeight()/2 - GetSpriteHeight(3)/2
		Player1Score = Player1Score + 1 // player 2 gets a point
		
		// the starting direction of the ball is randomized
		DRIX = Random (0, 1)
		DRIY = Random (0, 1)
		
		// player 2 score is displayed
		SetTextString(11, str(Player1Score))
		
		BallSpeed = 10 // the ball speed is reset
		Playerspeed = 10 // the players speeds are reset
		
		Playerspeed = 10 // the players speeds are reset
		Powergiven = 0 // no power up has be given 
		Powergiven1 = 0 // player 1 dose not have power up 
		Powergiven2 = 0 // player 2 dose not have power up 
		ResetTimer() // resets the timer use to display the power up 
		SetSpriteVisible(4, 0) // power up is invisible
		
		// Players paddles are the same 
		Player1_h = 125
		Player2_h = 125
		
		// both playes is repotioned in the middle for both sides 
		Player_1y = GetVirtualHeight() / 2 - GetSpriteHeight(1) / 2
		Player_2y = GetVirtualHeight() / 2 - GetSpriteHeight(2) / 2
	else
		// otherwise all of the variables stays the same
		Ball_x = Ball_x
		Player_1y = Player_1y
		Player_2y = Player_2y
		Ball_y = Ball_y
		Player1Score = Player1Score 
		Player2Score = Player2Score 
		BallSpeed = BallSpeed
		Playerspeed = Playerspeed
	endif
endif

SetSpriteSize(1, 10, Player1_h)
SetSpriteSize(2, 10, Player2_h)
SetSpritePosition(1, Player_1x, Player_1y)
SetSpritePosition(2, Player_2x, Player_2y)
SetSpritePosition(3, Ball_x, Ball_y)
return

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Exit_Game:
if GetRawKeyState(18) = 1 and GetRawKeyState(115) = 1 // if ALT and F4 is pressed together then it ends he game
	end
else
	Game_Play = Game_Play // otherwise the game gose on
endif
return

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Ball_Speed_up:
if mod(GetSeconds(),10) = 9 and count = 1// at exactly every 5 seconds 
	BallSpeed = BallSpeed + 3 // the ball speeds up
	Playerspeed = Playerspeed + 4 // the player's speed increases
	count = 0
else 
	if mod(GetSeconds(), 10) =  0 // reseting counting
		count = 1
	else
		count = count
	endif
endif

if BallSpeed > 20 // the maximum ball speed is 20 
	BallSpeed = 20
else
	if Playerspeed > 30 // the maximum player speed is 30
		Playerspeed = 30
	else
		// otherwise they stay the same
		Playerspeed = Playerspeed 
		BallSpeed = BallSpeed
	endif
endif
return

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Play_Again:
if GetRawKeyState(89) = 1 // IF Y (YES) is pressed //
	Player1Score = 0 // Player 1 score is 1 //
	Player2Score = 0 // Player 2 score is 0 //
	SetSpriteVisible(1, 1) // Player 1 paddle is shown //
	SetSpriteVisible(2, 1) // Player 2 paddle is shown //
	SetSpriteVisible(3, 1) // Ball is shown //
	SetSpriteVisible(4, 0) // Power up is hiddin //
	SetTextVisible(1, 0) // Main Menu Info is not shown //
	SetTextVisible(2, 0) // Main Menu Info is not shown //
	SetTextVisible(3, 0) // Main Menu Info is not shown //
	SetTextVisible(4, 0) // Main Menu Info is not shown //
	SetTextVisible(5, 0) // Normal Mode info is not shown //
	SetTextVisible(6, 0) // Normal Mode info is not shown //
	SetTextVisible(7, 0) // Normal Mode info is not shown //
	SetTextVisible(8, 0) // Normal Mode info is not shown //
	SetTextVisible(9, 0) // Normal Mode info is not shown //
	SetTextVisible(10, 0) // Normal Mode info is not shown //
	SetTextVisible(13, 0) // Player 1 Win Text is not shown //
	SetTextVisible(14, 0) // Player 2 Win Text is not shown //
	SetTextVisible(15, 0) // Play Again Text is not shown //
	SetTextVisible(16, 0) // Endless mode info is not shown //
	SetTextVisible(17, 0) // Endless mode info is not shown //
	SetTextVisible(18, 0) // Endless mode info is not shown //
	SetTextVisible(19, 0) // Endless mode info is not shown //
	SetTextVisible(20, 0) // Endless mode info is not shown //
	SetTextVisible(21, 0) // Endless mode info is not shown //
	Speed = 10 // reset ball speed //
else
	if GetRawKeyState (78) = 1 // IF N (NO) is pressed //
		end // ends the game //
	else
		Speed = 0 // the ball dose not move //
	endif
endif
SetTextString(11, str(Player1Score)) // display player 1 score //
SetTextString(12, str(Player2Score)) // display player 2 score //
SetSpritePosition(3, Ball_x, Ball_y) // set ball position //
return

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

// when player 2 gets upgrade //
Player_2_upgrade:

Player1_h = 125 // Player 1 height stays the same //
Player2_h = GetVirtualHeight() // Player 2 height is big as the height of the screen //
SetSpriteSize(1, 10, Player1_h) 
SetSpriteSize(2, 10, Player2_h)
SetSpriteVisible(4, 0) // the power up is invisible

return

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

// when player 1 gets upgrade //
Player_1_upgrade:

Player1_h = GetVirtualHeight() // Player 1 height is big as the height of the screen //
Player2_h = 125 // Player 2 height stays the same //
SetSpriteSize(1, 10, Player1_h)
SetSpriteSize(2, 10, Player2_h)
SetSpriteVisible(4, 0) // the power up is invisible

return 

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Power_up:

if timer() > 60.0 // if it has been more than 1 min
	Powergiven = 0 // no power is given 
	Powergiven1 = 0 // Player 1 has no power 
	Powergiven2 = 0 // Player 2 has no poer
	ResetTimer() // resets the timer use to display the power up  
	SetSpriteVisible(4, 0) // power up is not shown
	
	// Both player's height changes to the original height //
	Player1_h = 125
	Player2_h = 125
	SetSpriteSize(1, 10, Player1_h)
	SetSpriteSize(2, 10, Player2_h)
	
	// Both player's is placed in the middle in their repective sides
	Player_1x = 10 
	Player_1y = GetVirtualHeight() / 2 - GetSpriteHeight(1) / 2
	SetSpritePosition(1, Player_1x, Player_1y)
	Player_2x = GetVirtualWidth() - GetSpriteWidth(2) - 10
	Player_2y = GetVirtualHeight() / 2 - GetSpriteHeight(2) / 2
	SetSpritePosition(2, Player_2x, Player_2y)
else
	// otherwise all of the variables stays the same
	Powergiven = Powergiven
	Powergiven1 = Powergiven1
	Powergiven2 = Powergiven2
	SetSpriteSize(1, 10, Player1_h)
	SetSpriteSize(2, 10, Player2_h)
endif 


if Powergiven = 0 // if power up has not been given
	if timer() > 10.0 // if the game is on for more than 10 second
		SetSpriteVisible(4, 1) // power up is visible
		if GetSpriteCollision(3, 4) = 1 and DRIX = -1 // if the ball hits the power up and is moving left
			gosub Player_2_upgrade // player 2 get power up
			Powergiven = 1 // power up has been given
			Powergiven2 = 1 // player 2 keep the power up
		else
			if GetSpriteCollision(3 ,4) = 1 and DRIX = 1 // if the ball hits the power up and is moving right
				gosub Player_1_upgrade // player 1 het the upgrade
				Powergiven = 1 // power up has been given
				Powergiven1 = 1 // player 1 keeps the power up
			else
				// otherwise all of the variables stays the same
				Powergiven = Powergiven
				Powergiven1 = Powergiven1
				Powergiven2 = Powergiven2
			endif
		endif
	else
		SetSpriteVisible(4, 0) // power up is not visible
	endif
else
	if Powergiven = 1 // if power up has been given
		SetSpriteVisible(4, 0) // power up is invisible
		if timer() > 10.0 // if the game is on for more than 10 second
			if Powergiven2 = 1 // if Player 2 got the power up first
				gosub Player_2_upgrade // Plyaer 2 keep the power up
			else
				if Powergiven1 = 1 // if Player 1 got the power up first
					gosub Player_1_upgrade // player 1 keeps the power up
				else
					// otherwise all of the variables stays the same
					Powergiven = Powergiven
					Powergiven1 = Powergiven1
					Powergiven2 = Powergiven2
				endif
			endif
		else
			SetSpriteVisible(4, 0) // power up is invisible
			// otherwise all of the variables stays the same
			Powergiven = Powergiven
			Powergiven1 = Powergiven1
			Powergiven2 = Powergiven2
		endif
	else
		// otherwise all of the variables stays the same
		Powergiven = Powergiven
		Powergiven1 = Powergiven1
		Powergiven2 = Powergiven2
	endif
endif
return

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
// End of Code                                                                                                                                                                                                    / ////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
