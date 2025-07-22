## PROJECT_SOURCE:

C:\Users\Gabe\source\repos\gemini-api-paid-tier-upgrade\ImThatKidAI

## FEATURE:

Make my text to speech more stable, and more user friendly. Right now it works, but it has some glitches every once in a while, like the stop speech button not working sometimes, or speech not playing, or speech continuing to play when I switch tabs or switch apps. I want the text to speech to always work, and always work well. Analyze the project, and how the test to speech works, and how we can improve it.

## RELEVANT_CODE:

TTSService.cs - helps control TTS
MainPage.cs - uses TTS for messages
SecureSpeechService.cs - helps control TTS
TutorialService.cs - uses TTS for messages
ChatRegistrationPage.xaml.cs - uses TTS for messages

## EXAMPLES:

## DOCUMENTATION:

## OTHER CONSIDERATIONS:

Do not lose any existing TTS functionality. It works now, it just is not the most stable.
Make sure to update the README in the project to document how the TTS works.