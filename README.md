# CodeStudioDevLog_Year1

# TODO: Delete this information when it is practiced enough to become useless
The purpose of this devlog is to form the assessment submission for my Code Studio module. It must be reflective rather than descriptive, and it will be marked according to this grading scale:
![image](https://github.com/user-attachments/assets/d6b3b1af-2c1e-4889-a8b5-8185159ba1ac)


after looking at the reflective writing example it appears to follow this structure

1 research and methodology followed when approaching the task

2 problems that appeared (only major problems not i couldnt find the documentation), highlight where the research differs from reality

3 methodology of fixing the issue along with any data and research to support

4 what went well/wrong in both your original approach and how you fixed any issues

5 how would you handle this next time based on what you have learned

6 reference list

# DevLog Start

I have started researching how a rhythm game would work within UE5 opting to use C++ to maximise the learning possible within the confines of the project. After some research (https://www.youtube.com/watch?v=FgR35xDWbw4 and https://www.youtube.com/watch?v=F0PFHXUfa2Y among others) found that the best solution was to synchronise the code with the music through events trigerred in a level sequence, opting to keep it simple I had seperate events to open and close the hit window for each note however to impliment it fully I will change it to one event which opens and closes the window itself so that the gap can be consistent and I can make it modeular for difficulty settings. I found most of the documentation I need is hidden away which is where forums like r/unrealengine and stack overflow are valuable resources.

consolidation week

over the consolidation week i have worked extensively on the second game jam "shoot 'em up" where the teaching I have received already has been invaluable, not just for bug fixing in the discord but the additional coding for cool kids club, what was posed as a solution for radial menu's (ATan2) came in handy for creating the aiming for a twin stick style shooter:

/*
FRotator ALightsCameraActionCharacter::GetAimRotation()
{
	// finds mouse position in viewport
	float MouseX;
	float MouseY;
	UGameplayStatics::GetPlayerController(GetWorld(), 0)->GetMousePosition(MouseX, MouseY);
	
	// finds radians and angle of mouse from the centre of screen
	float AimRadians = atan2((MouseY-ViewportCenter.Y), (MouseX-ViewportCenter.X));
	FRotator AimRotation = FRotator(0.f, (AimRadians*180/PI)+90, 0);

	// makes the aim rotation the same notation as the component rotation (-180 to 180)
	if (AimRotation.Yaw > 180)
	{
		AimRotation.Yaw -= 360;
	}
	
	return AimRotation;
}
*/
