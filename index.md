


<p></p>

## Overview
<p align="justify">
This paper introduces PFlow-VC, a conditional flow matching voice conversion model that leverages fine-grained discrete pitch tokens and target speaker prompt information for expressive voice conversion (VC). Previous VC works primarily focus on speaker conversion, with further exploration needed in enhancing expressiveness (such as prosody and emotion) for timbre conversion. Unlike previous methods, we adopt a simple and efficient approach to enhance the style expressiveness of voice conversion models. Specifically, we pretrain a self-supervised pitch VQVAE model to discretize speaker-irrelevant pitch information and leverage a masked pitch-conditioned flow matching model for Mel-spectrogram synthesis, which provides in-context pitch modeling capabilities for the speaker conversion model, effectively improving the voice style transfer capacity. Additionally, we improve timbre similarity by combining global timbre embeddings with time-varying timbre tokens. Experiments on unseen LibriTTS test-clean and emotional speech dataset ESD show the superiority of the PFlow-VC model in both timbre conversion and style transfer.
</p>


## Model Architecture
<table>
    <tr>
        <td ><center><img src="assets/image/archi.png"/> </center></td>
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
