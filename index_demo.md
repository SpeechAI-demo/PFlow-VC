


<p></p>

## Overview
<p align="justify">
Controllable text-to-speech (TTS) aims to achieve flexible and accurate control, 
synthesizing speech across various domains. 
Several recent works adopting natural language descriptions to control speech attributes has gained 
much attention. However, achieving accurate timbre control when utilizing text to manipulate speech 
style poses significant challenges. In light of this, 
we propose VS-TTS, a multi-modal prompt speech synthesis system that allows user-friendly control 
over voice styles while maintain speaker identity. 
Specifically, 1) We present the baseline model for the VS-TTS task, providing detailed descriptions of dataset preprocessing. 
2) We employ a BERT-based text prompt encoder to extract a fixed-length speaking-style-correlated hidden. For speaker prompt, we leverage a multi-stream transformer encoder to learn diverse speaker attributes from multiple views and thus improve speaker similarity. 3) To improve style expressiveness and alleviate one-to-many problem, we introduce a diffusion-based Variation Enhance Network to provide finer grained additional variability information as a supplement for those acoustic features not coverage in natural language prompts. Our extensive evaluations in audiobook dataset (LibriTTS) and multi-corpus emotional datasets demonstrate that VS-TTS outperforms baseline models in terms of style controllability and speaker similarity.
</p>

## Model Architecture
<table>
    <tr>
        <td ><center><img src="assets/image/figure1.png"/> </center></td>
    </tr>
</table>
<p align="center">Figure.1 The overall architecture of PFlow-VC.</p>



<script>
function pauseOthers(ele) {
    $("audio").not(ele).each(function (index, audio) {audio.pause();});
}
</script>

<style>
.main-content table {
    display: inline-table;
}
table {
    table-layout:fixed;
    width: 100%;
    overflow: hidden;
}
#player{
    width: 100%;
}
</style>
<p>&nbsp;</p> 







##  1. LibriTTS seen case

### Attribure Control

####  1.1 Volume

Volume-1: *A speaker is speaking **softly**: His eyes, which are hazel, are remarkably bright; he has a sight keen as a hawk's.*

Volume-2: *The speaker speaks  with **normal energy**: His eyes, which are hazel, are remarkably bright; he has a sight keen as a hawk's.*

Volume-3: *A speaker with a **vibrant** voice: His eyes, which are hazel, are remarkably bright; he has a sight keen as a hawk's.*

<table>
    <tr>
        <th> Volume</th>
        <th>Audio Prompt</th>
        <th> VS-TTS</th>
        <th> InstructTTS</th>
        <th> PromptStyle</th>
    </tr>
    <tr>
        <th> 1</th>
        <th rowspan='3'> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/volume/audio_prompt.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/volume/vstts-energy-low.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/volume/instruct-energy-low.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/volume/style-energy-low.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> 2</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/volume/vstts-energy-normal.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/volume/instruct-energy-normal.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/volume/style-energy-normal.wav" type="audio/mpeg"></audio> </th>
    </tr>	
    <tr>
        <th> 3</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/volume/vstts-energy-high.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/volume/instruct-energy-high.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/volume/style-energy-high.wav" type="audio/mpeg"></audio> </th>
    </tr>	
</table>



#### 1.2 Speed

Speed-1: *The speaker spoke at a **slow pace**: Spargo, much astonished at this reception, passed through an ante room into a handsomely furnished apartment full of books and pictures.*

Speed-2: *The speaker spoke at a **normal pace**: Spargo, much astonished at this reception, passed through an ante room into a handsomely furnished apartment full of books and pictures.*

Speed-3: *The speaker spoke at a **fast pace**: Spargo, much astonished at this reception, passed through an ante room into a handsomely furnished apartment full of books and pictures.*

<table>
    <tr>
        <th> Speed</th>
         <th>Audio Prompt</th>
        <th> VS-TTS</th>
        <th> InstructTTS</th>
        <th> PromptStyle</th>
    </tr>
    <tr>
        <th> 1</th>
        <th rowspan='3'> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/speed/audio_prompt.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/speed/vstts-dur-low.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/speed/instruct-dur-low.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/speed/style-dur-low.wav" type="audio/mpeg"></audio> </th>
    </tr>	
    <tr>
        <th> 2</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/speed/vstts-dur-normal.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/speed/instruct-dur-normal.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/speed/style-dur-normal.wav" type="audio/mpeg"></audio> </th>
    </tr>	
    <tr>
        <th> 3</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/speed/vstts-dur-high.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/speed/instruct-dur-high.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source 
src="assets/audios/libritts(seen)/speed/style-dur-high.wav" type="audio/mpeg"></audio> </th>
    </tr>	
</table>



#### 1.3 Pitch

Pitch-1: *The speaker says with a **low-key voice**: The King of the Golden River had hardly made the extraordinary exit related in the last chapter, before Hans and Schwartz came roaring into the house very savagely drunk.*

Pitch-2: *The speaker says with a **normal-key voice**: The King of the Golden River had hardly made the extraordinary exit related in the last chapter, before Hans and Schwartz came roaring into the house very savagely drunk.*

Pitch-3: *The speaker says with a **high-key voice**: The King of the Golden River had hardly made the extraordinary exit related in the last chapter, before Hans and Schwartz came roaring into the house very savagely drunk.*

<table>
    <tr>
        <th> Pitch</th>
         <th>Audio Prompt</th>
        <th> VS-TTS</th>
        <th> InstructTTS</th>
        <th> PromptStyle</th>
    </tr>
    <tr>
        <th> 1</th>
        <th rowspan='3'> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/pitch/audio_prompt.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/pitch/vstts-pitch-low.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/pitch/instruct-pitch-low.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/pitch/style-pitch-low.wav" type="audio/mpeg"></audio> </th>
    </tr>	
    <tr>
        <th> 2</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/pitch/vstts-pitch-normal.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/pitch/instruct-pitch-normal.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/pitch/style-pitch-normal.wav" type="audio/mpeg"></audio> </th>
    </tr>	
    <tr>
        <th> 3</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/pitch/vstts-pitch-high.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(seen)/pitch/instruct-pitch-high.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source 
src="assets/audios/libritts(seen)/pitch/style-pitch-high.wav" type="audio/mpeg"></audio> </th>
    </tr>	
</table>


<p>&nbsp;</p> 

## 2. LibriSpeech test-clean(unseen case)

###  2.1 Attribute Control 

#### Volume

Volume-1: *A speaker is speaking **softly**: It was a long ride over the circuitous route by which the steep incline was avoided and it was necessary for the party to make an early start.*

Volume-2: *The speaker speaks  with **normal energy**: It was a long ride over the circuitous route by which the steep incline was avoided and it was necessary for the party to make an early start.*

Volume-3: *A speaker with a **vibrant** voice: It was a long ride over the circuitous route by which the steep incline was avoided and it was necessary for the party to make an early start.*

<table>
    <tr>
        <th> Model</th>
         <th>Audio Prompt</th>
        <th>Volume-1</th>
        <th> Volume-2</th>
        <th> Volume-3</th>
    </tr>
    <tr>
        <th>VS-TTS</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/volume/audio_prompt.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/volume/vstts-energy-low.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/volume/vstts-energy-normal.wav" type="audio/mpeg"></audio> </th>
         <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/volume/vstts-energy-high.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>



#### Speed

Speed-1: *The speaker spoke at a **slow pace**: The judge refused to admit his evidence, on the ground that the witness had destroyed beforehand all the confidence of the Court in what he was about to say.*

Speed-2: *The speaker spoke at a **normal pace**: The judge refused to admit his evidence, on the ground that the witness had destroyed beforehand all the confidence of the Court in what he was about to say.*

Speed-3: *The speaker spoke at a **fast pace**: The judge refused to admit his evidence, on the ground that the witness had destroyed beforehand all the confidence of the Court in what he was about to say.*

<table>
    <tr>
        <th> Model</th>
         <th>Audio Prompt</th>
        <th>Speed-1</th>
        <th>Speed-2</th>
        <th>Speed-3</th>
    </tr>
    <tr>
        <th>VS-TTS</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/speed/audio_prompt.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/speed/vstts-dur-low.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/speed/vstts-dur-normal.wav" type="audio/mpeg"></audio> </th>
         <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/speed/vstts-dur-high.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>



#### Pitch

Pitch-1: *The speaker says with a **low-key voice**: But upon the question of labour mr Grammont was fierce, even for an American business man, and one night at a dinner party he discovered his daughter displaying what he considered an improper familiarity with socialist ideas.*

Pitch-2: *The speaker says with a **normal-key voice**: But upon the question of labour mr Grammont was fierce, even for an American business man, and one night at a dinner party he discovered his daughter displaying what he considered an improper familiarity with socialist ideas.*

Pitch-3: *The speaker says with a **high-key voice**: But upon the question of labour mr Grammont was fierce, even for an American business man, and one night at a dinner party he discovered his daughter displaying what he considered an improper familiarity with socialist ideas.*

<table>
    <tr>
        <th> Model</th>
         <th>Audio Prompt</th>
        <th>Pitch-1</th>
        <th>Pitch-2</th>
        <th>Pitch-3</th>
    </tr>
    <tr>
        <th>VS-TTS</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/pitch/audio_prompt.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/pitch/vstts-pitch-low.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/pitch/vstts-pitch-normal.wav" type="audio/mpeg"></audio> </th>
         <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/pitch/vstts-pitch-high.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>



### 2.2 Attribute Control with unseen speaker

#### **sample1**

With a low voice, the speaker engages in quick speech while maintaining usual vitality.

1. mrs Harker began to blush, and taking a paper from her pockets, she said:
2. The King of the Golden River had hardly made the extraordinary exit related in the last chapter, before Hans and Schwartz came roaring into the house very savagely drunk.
3. Dykvelt, whose adroitness and intimate knowledge of English politics made his assistance, at such a conjuncture, peculiarly valuable, was one of the Ambassadors; and with him was joined Nicholas Witsen, a Burgomaster of Amsterdam, who seems to have been selected for the purpose of proving to all Europe that the long feud between the House of Orange and the chief city of Holland was at an end.

<table>
    <tr>
         <th>Audio Prompt: </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/1/audio_prompt1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/1/audio_prompt2.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/1/audio_prompt3.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th>VS-TTS</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/1/gen1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/1/gen2.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/1/gen3.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>

<p>&nbsp;</p> 

#### **sample2**

The speaker says quickly but in a quiet manner.

1. But it isn't good manners to tell your company what you are going to give them to eat, so I won't tell you what she said we could have to drink.
2. His own possessions, safety, life, he would have hazarded for Lucie and her child, without a moment's demur; but the great trust he held was not his own, and as to that business charge he was a strict man of business.
3. "But, Pencroft," answered Spilett, "you are describing a picture of the Creator."

<table>
    <tr>
         <th>Audio Prompt: </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/2/audio_prompt1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/2/audio_prompt2.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/2/audio_prompt3.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th>VS-TTS</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/2/gen1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/2/gen2.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/2/gen3.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>



#### **sample3**

Speaking slowly, the speaker had a high-pitched voice and a quiet, low-energy aura.

1. But it isn't good manners to tell your company what you are going to give them to eat, so I won't tell you what she said we could have to drink.
2. His own possessions, safety, life, he would have hazarded for Lucie and her child, without a moment's demur; but the great trust he held was not his own, and as to that business charge he was a strict man of business.
3. Hugh told him the name; and then made him look with the telescope all along the receding line to the trees on the opposite hill.

<table>
    <tr>
         <th>Audio Prompt: </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/3/audio_prompt1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/3/audio_prompt2.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/3/audio_prompt3.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th>VS-TTS</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/3/gen1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/3/gen2.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/libritts(unseen)/control_with_timbre/3/gen3.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>


## 3. Emotional Speech Dataset test

#### **sample1**

Text prompt：A **amazed** speaker's energetic high pitch electrifies and enlivens the listeners.

Text：To catch that bulrush root with my paw

<table>
    <tr>
         <th>Audio Prompt</th>
        <th>VS-TTS</th>
        <th>InstructTTS</th>
        <th>PromptStyle</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/audio_prompt1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/vstts-1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/instruct-1.wav" type="audio/mpeg"></audio> </th>
         <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/style-1.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>



#### **sample2**

Text prompt：With speaker's distinctive deep voice, speaker **sadly** converses at a moderate speed and standard energy levels.

Text：But the ships are very slow now and we don't get so many sailors any more.

<table>
    <tr>
         <th>Audio Prompt</th>
        <th>VS-TTS</th>
        <th>InstructTTS</th>
        <th>PromptStyle</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/audio_prompt2.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/vstts-2.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/instruct-2.wav" type="audio/mpeg"></audio> </th>
         <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/style-2.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>



#### **sample3**

Text prompt：With normal pitch, the **furious** speaker delivers an animated speech at a regular pace.

Text：Don't ask me to carry an oily rag like that.

<table>
    <tr>
         <th>Audio Prompt</th>
        <th>VS-TTS</th>
        <th>InstructTTS</th>
        <th>PromptStyle</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/audio_prompt3.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/vstts-3.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/instruct-3.wav" type="audio/mpeg"></audio> </th>
         <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/style-3.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>



#### **sample4**

Text prompt：The **afraid** speaker swiftly expressed

Text：Dogs are sitting by the door.

<table>
    <tr>
         <th>Audio Prompt</th>
        <th>VS-TTS</th>
        <th>InstructTTS</th>
        <th>PromptStyle</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/audio_prompt4.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/vstts-4.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/instruct-4.wav" type="audio/mpeg"></audio> </th>
         <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/style-4.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>



#### **sample5**

Text prompt：The speaker **gleefully** talks at a normal pace.

Text：Zero four three a silver shilling is journey.

<table>
    <tr>
         <th>Audio Prompt</th>
        <th>VS-TTS</th>
        <th>InstructTTS</th>
        <th>PromptStyle</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/audio_prompt5.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/vstts-5.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/instruct-5.wav" type="audio/mpeg"></audio> </th>
         <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/emotion/style-5.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>





## 4.Non-reading-style speech dataset test

#### Speed

Speed-1: *The speaker spoke at a **slow pace**: The judge refused to admit his evidence, on the ground that the witness had destroyed beforehand all the confidence of the Court in what he was about to say.*

Speed-2: *The speaker spoke at a **normal pace**: The judge refused to admit his evidence, on the ground that the witness had destroyed beforehand all the confidence of the Court in what he was about to say.*

Speed-3: *The speaker spoke at a **fast pace**: The judge refused to admit his evidence, on the ground that the witness had destroyed beforehand all the confidence of the Court in what he was about to say.*

<table>
    <tr>
        <th> LRS3 Speaker</th>
         <th>Audio Prompt</th>
        <th>Speed-1</th>
        <th>Speed-2</th>
        <th>Speed-3</th>
    </tr>
    <tr>
        <th>o1Z4F4e2Bw4_00003</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/speed/o1Z4F4e2Bw4_00003/00003.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/speed/o1Z4F4e2Bw4_00003/gen_wav_6.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/speed/o1Z4F4e2Bw4_00003/gen_wav_7.wav" type="audio/mpeg"></audio> </th>
         <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/speed/o1Z4F4e2Bw4_00003/gen_wav_8.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th>k2hQL9Zrokk_00002</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/speed/k2hQL9Zrokk_00002/00002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/speed/k2hQL9Zrokk_00002/gen_wav_6.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/speed/k2hQL9Zrokk_00002/gen_wav_7.wav" type="audio/mpeg"></audio> </th>
         <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/speed/k2hQL9Zrokk_00002/gen_wav_8.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>


#### Pitch

Pitch-1: *The speaker says with a **low-key voice**: But upon the question of labour mr Grammont was fierce, even for an American business man, and one night at a dinner party he discovered his daughter displaying what he considered an improper familiarity with socialist ideas.*

Pitch-2: *The speaker says with a **normal-key voice**: But upon the question of labour mr Grammont was fierce, even for an American business man, and one night at a dinner party he discovered his daughter displaying what he considered an improper familiarity with socialist ideas.*

Pitch-3: *The speaker says with a **high-key voice**: But upon the question of labour mr Grammont was fierce, even for an American business man, and one night at a dinner party he discovered his daughter displaying what he considered an improper familiarity with socialist ideas.*

<table>
    <tr>
        <th> LRS3 Speaker</th>
         <th>Audio Prompt</th>
        <th>Pitch-1</th>
        <th>Pitch-2</th>
        <th>Pitch-3</th>
    </tr>
    <tr>
        <th>GSf6nijSSdA_00004</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/pitch/GSf6nijSSdA_00004/00004.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/pitch/GSf6nijSSdA_00004/gen_wav_3.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/pitch/GSf6nijSSdA_00004/gen_wav_4.wav" type="audio/mpeg"></audio> </th>
         <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/pitch/GSf6nijSSdA_00004/gen_wav_5.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th>UMhLBPPtlrY_00004</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/pitch/UMhLBPPtlrY_00004/00004.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/pitch/UMhLBPPtlrY_00004/gen_wav_3.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/pitch/UMhLBPPtlrY_00004/gen_wav_4.wav" type="audio/mpeg"></audio> </th>
         <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/pitch/UMhLBPPtlrY_00004/gen_wav_5.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>



#### Volume

Volume-1: *A speaker is speaking **softly**: It was a long ride over the circuitous route by which the steep incline was avoided and it was necessary for the party to make an early start.*

Volume-2: *The speaker speaks  with **normal energy**: It was a long ride over the circuitous route by which the steep incline was avoided and it was necessary for the party to make an early start.*

Volume-3: *A speaker with a **vibrant** voice: It was a long ride over the circuitous route by which the steep incline was avoided and it was necessary for the party to make an early start.*

<table>
    <tr>
        <th> LRS3 Speaker</th>
         <th>Audio Prompt</th>
        <th>Volume-1</th>
        <th> Volume-2</th>
        <th> Volume-3</th>
    </tr>
    <tr>
        <th>jcp5vvxtEaU_00001</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/volume/jcp5vvxtEaU_00001/00001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/volume/jcp5vvxtEaU_00001/gen_wav_0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/volume/jcp5vvxtEaU_00001/gen_wav_1.wav" type="audio/mpeg"></audio> </th>
         <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/volume/jcp5vvxtEaU_00001/gen_wav_2.wav" type="audio/mpeg"></audio> </th>
    </tr>
     <tr>
        <th>y6MC4iXhT6I_00001</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/volume/y6MC4iXhT6I_00001/00001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/volume/y6MC4iXhT6I_00001/gen_wav_0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/volume/y6MC4iXhT6I_00001/gen_wav_1.wav" type="audio/mpeg"></audio> </th>
         <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="./assets/audios/lrs3/volume/y6MC4iXhT6I_00001/gen_wav_2.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>





##  5.More samples

**sample1**

Text prompt：Rapid speech with a high key characterizes speaker's conversation style.

Text：She tied the unhappy dog up again, but do you think Nana ceased to bark? Bring master and missus home from the party!

<table>
    <tr>
         <th>Audio Prompt</th>
        <th>VS-TTS</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/rebuttal/sample1/audio_prompt.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/rebuttal/sample1/vstts.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>




**sample2**

Text prompt：A amazed speaker voice, low in pitch, speaks quickly while exuding normal energy.

Text：Come on my jack in the boxes!

<table>
    <tr>
         <th>Audio Prompt</th>
        <th>VS-TTS</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/rebuttal/sample2/audio_prompt.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/rebuttal/sample2/vstts.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>




**sample3**

Text prompt：Speaking quickly and with a deep pitch, speaker sustains a normal level of vitality.

Text：I ran back to the entrance compartment.

<table>
    <tr>
         <th>Audio Prompt</th>
        <th>VS-TTS</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/rebuttal/sample3/audio_prompt.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/rebuttal/sample3/vstts.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>




**sample4**

Text prompt：In speaker's conversation, the speaker utilizes a standard pitch, conversing at a moderate pace, and exuding low energy.

Text：It was not the first time that I had helped him and been well paid for my help.

<table>
    <tr>
         <th>Audio Prompt</th>
        <th>VS-TTS</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/rebuttal/sample4/audio_prompt.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/rebuttal/sample4/vstts.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>




**sample5**

Text prompt：speaker's speech maintains a usual pitch as speaker mournfully talks at a regular speed with a touch of standard energy.

Text：They'd never know I'd regular ran away.

<table>
    <tr>
         <th>Audio Prompt</th>
        <th>VS-TTS</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/rebuttal/sample5/audio_prompt.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/rebuttal/sample5/vstts.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>




**sample6**

Text prompt：A  speaker talks quickly in a hushed manner.

Text：In the healthy marriage, this sympathetic response will soon give way to anger, which in turn may have the effect of a dash of cold water in the face of the oversensitive one, helping him or her to buck up and behave like an adult.

<table>
    <tr>
         <th>Audio Prompt</th>
        <th>VS-TTS</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/rebuttal/sample6/audio_prompt.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/rebuttal/sample6/vstts.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>



**sample7**

Text prompt：Rapid-speaking speaker in a quiet manner.

Text：In the daytime she sat down once more beneath the windows of the castle, and began to card with her golden carding comb; and then all happened as it had happened before. 

<table>
    <tr>
         <th>Audio Prompt</th>
        <th>VS-TTS</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/rebuttal/sample7/audio_prompt.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/rebuttal/sample7/vstts.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>


