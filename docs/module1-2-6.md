# Module 1.2: Activity

!!! question "Analyse this study design"
    

    **Study design**

    For the mouse transplantation experiment in a 2012 study, researchers used stool samples from the **same five women** in early pregnancy (**T1**) and late pregnancy (**T3**).

    They combined the samples into **one mixture per trimester** and gave each mixture to germ-free mice.
    
    The fat-gain analysis included six mice receiving the T1 mixture and five receiving the T3 mixture, after one T3 mouse was excluded as an outlier.

    **Research question**

    Does gut microbiota from late pregnancy cause greater fat gain in mice than microbiota from early pregnancy, and does this effect hold across different women?

    ![](figs_m1/01_pseudoreplication_activity01_v01.png){width=90%}

    <small>Ref: [Koren et al., *Cell* 150, 470–480 (2012), Figure 6C](https://pmc.ncbi.nlm.nih.gov/articles/PMC3505857/#F6)</small>

    **Discuss in your group**

    1. Can this design show that the effect holds across different women?
    2. Do mice receiving the same mixture count as independent donor replicates?
    3. For this research question, should **n** count the mice or the donor pools?
    4. Can reanalysis fix the missing donor replication, or are new experiments needed?

<!-- 
??? success "Answers: reveal after group discussion"

    **1. Can this design show that the effect holds across different women?**

    No. There is only **one mixture per trimester**, so we cannot assess how the transplantation effect varies between women.

    **2. Do the mice count as independent donor replicates?**

    No. Every mouse in a group received the same mixture. Differences between them reflect mouse-to-mouse responses to that mixture, not differences between women.

    **3. Should n count mice or independent donor pools?**

    For this donor-level question, count **independent donor pools: n = 1 per trimester**.

    The mouse-level analysis can still test whether these two mixtures affect mice differently. It cannot establish whether the effect holds across different women. More mice do not increase donor replication.

    **4. Can reanalysis fix this?**

    **New transplantation experiments are needed**, using separate donor samples. Reanalysis cannot recover donor-specific effects that were never measured.

    **Take-home message**

    More mice receiving the same mixture cannot replace independent replication across donors.

-->
<!-- FACILITATOR NOTES — NOT DISPLAYED Main message ------------ Keep the discussion focused on the stated question: does the transplantation effect hold across different women? The experiment measures responses to two mixtures. It does not measure separate transplantation effects across donors. If someone asks: “How can you do statistics with n = 1?” ------------------------------------------------------- Say: “We cannot estimate variation across donor pools with only one pool per trimester. The published analysis uses variation between mice, which answers a narrower question.” If someone asks: “So was the study wrong?” ------------------------------------------ Say: “We are examining the limits of this transplantation experiment, not judging the whole paper. The mouse comparison can provide evidence about these two mixtures. It cannot establish that the effect holds across women. The paper also contains a separate human-cohort analysis.” If someone says: “The mouse is the experimental unit” ----------------------------------------------------- Ask: “An experimental unit for which comparison?” Explain: “That can be correct for comparing the two mixtures, if allocation and housing support independence. But another mouse receiving the same mixture does not add another independent donor pool.” If someone calls the mice technical replicates ----------------------------------------------- Say: “They are different animals with real variation in their responses. They are not repeated measurements of the same sample. But they all received the same donor mixture within each group.” If someone asks whether donor sequencing could fix this -------------------------------------------------------- Say: “The authors sequenced individual donor samples as well as the mixtures. That tells us about the microbiomes. It does not tell us how each donor's sample would have affected mice if transplanted separately.” Suitable retained samples could support new transplantation experiments; they cannot repair the existing mouse data through reanalysis. If someone notices the paired design -------------------------------------- Say: “The same women contributed at both timepoints, so donor identity is held constant. Pooling still prevents us from measuring the transplantation effect separately for each woman.” If housing or the excluded mouse comes up ------------------------------------------- Housing and allocation matter for mouse independence. Do not assume the housing arrangement from the activity figure. Figure 6C reports six T1 mice and five T3 mice after one T3 outlier was removed. The legend alone does not establish whether that exclusion was justified. The donor-replication problem remains either way. Before displaying the figure ----------------------------- Ensure it shows the same five women contributing at T1 and T3, one mixture per trimester, and the correct analysed mouse numbers for Figure 6C. Do not label the mice as technical replicates. -->