# Sequence Tagged Gene Deletion
by Hector Burgos

This protocol details how to generate a clean deletion of target genes in *Vibrio fischeri* where each deletion strain is tagged with a unique sequence or "barcode".
SOE-PCR is used to generate the Mutagenic DNA (linear dsDNA carrying Erm<sup>R</sup> and the barcode, flanked by FRT sites and upstream and downstream homology to target gene; arranged as follows: US homology-FRT-Erm<sup>R</sup>-FRT-barcode-DS homology) and *tfoX* transformation is used to insert it into *V. fischeri* where it recombines into the chromosome based on sequence homology.
This technique then allows for the excision of the Erm<sup>R</sup> cassette by inserting a plasmid that expresses FLP recombinase, which uses the FRT sites to remove the antibiotic cassette.
The resulting scar is in-frame (reduces likelihood of polar effects on gene expression) and carries a barcode that allows identification of the specific deletion strain through sequencing.
One important detail is that the start codon and the last 7 codons (6 aa plus stop codon) of the targeted gene are preserved and form part of the deletion scar.
The overall approach is summarized below:

<IMG SRC="/images/sequence-tagged-gene-deletion/sequence-tagged-gene-deletion-approach.png" WIDTH=425>

## I - Oligo Design

<IMG SRC="/images/sequence-tagged-gene-deletion/Oligos-Gene-Deletion.png" WIDTH=900>
<br><br>
Oligos F1 and R1-LUH amplify 1Kb upstream of target gene including the start codon, while oligos F2-RUH and R2 amplify the 1 Kb downstream of target gene including the last 7 codons.
Oligo FO anneals 1.5 Kb upstream of target gene and is used to amplify from outside the junction of the mutation to verify insertion of cassette in correct genomic location.
Oligos FW and RW anneal within target gene and should produce no product from a successful gene deletion strain.

I use Benchling to design my oligos, so the following instructions are assuming you are also using Benchling.
Otherwise, you can adapt the oligo design to whatever approach you use.

1. Generate a sequence file containing the gene of interest and 2 Kb of flanking sequence.
2. Substitute the coding sequence of the target gene with the barcoded Erm<sup>R</sup>-Marker within the start codon and the last 7 codons (6 aa plus stop codon) of the gene of interest. [Example: Δ*cueR*::erm-bar.](https://benchling.com/s/seq-b4AyxNqFLv25wjchrTqZ)
3. Using the distances shown in the image above as a guide, design oligos with a Tm = 60 ± 3°C (verify Tm with the "Analyze" function of [IDT's OligoAnalyzer 3.1 tool](https://www.idtdna.com/calc/analyzer)). \*Make sure oligo R1 starts with the start codon of the target gene, while F2 should include the last 7 codons (6 aa plus stop codon).
4. Attach the reverse complement of LUH to the 5'-end of R1 and RUH to 5'-end of F2 to form the R1-LUH and F2-RUH oligos (LUH Reverse complement = CTGGCGAAGCATATATAAGAAGCTCGTCTCGT; RUH = GACTTGACCTGGATGTCTCTACCCACAAGATCG).
5. Calculate the predicted secondary structures for the oligos using the "Hairpin" function of [IDT's OligoAnalyzer 3.1 tool](https://www.idtdna.com/calc/analyzer) and reject oligos with predicted structures with a Tm ≥ ~45°C.

\* If you are working with FLP sites, avoid generating oligos to FLP sites.
Since it's a palindrome the oligo will likely form a hairpin and not work as intended in a PCR.

## II - Ordering Oligos

1. Sign in to [Shop@UW](https://mds.bussvc.wisc.edu/order/shopper_lookup.asp) using the Mandel Lab login, select "Shop at External Suppliers & UW-Madison MDS Warehouse",
 and navigate to IDT's webpage.
2. Under "Products & Services" tab, go to "Custom DNA oligos" and select "DNA oligos".
Oligos can be ordered in tubes or in 96-well plates (24 oligos minimum; select "all ordering options" when navigating to "DNA oligos").
3. For ordering multiple oligos:
  - In tubes: select "bulk input", download an oligo input template, fill in your oligos, then upload to IDT.
  - 96-well plate: select "upload plate", download the "Excel plate ordering template", fill in your oligos, and upload. Name your plate with a unique but simple name, as oligo location is entered into Mandel Lab database in the "Plate, well" format. Under "plate specifications", select "normalized yield" for "normalization type", and "calculate" the "quantity (nmol)" and input the max option (e.g., 4-5 nmol).

\* Oligos are generally ordered at the 25 nmole scale, where oligo size is limited to 60 bp for tubes and 80 bp for 96-well plate.
If oligos are larger than the allowed size (usually R1-LUH and F2-RUH), delete bases from the 5'-end of the oligo until size is reduced to the allowed size (up to 5 bp can be deleted without causing issues downstream; I haven't tested longer deletions); otherwise you can order in 100 nmole scale, though this is not recommended for plates as you will have to order a separate plate for each synthesis scale.

4. Once you are sure that your order is set up correctly, place order in IDT, which will take you back to Shop@UW, then follow the prompts to finish the order.
5. Record order in Mandel Lab supplies log.
6. Once oligos arrive, record order as received, add TE to 100 µM, then prepare 10 µM working dilutions of the oligos (when using plates, prepare the 10 µM working dilutions in 0.2 mL striptubes; this allows the use of a multichannel pipette and ensures appropriate storage of the oligos).

## III - Amplification of Upstream (US) and Downstream (DS) Homology Arms

In this section you will use PCR to generate DNA containing the upstream and downstream homology regions of your target gene.
You will use oligos F1 and R1-LUH to amplify the upstream region, and oligos F2-RUH and R2 to amplify the downstream region.
Each DNA fragment will contain the linker sequences (LUH or RUH, at the 3'-end of the upstream fragment or the 5'-end of the downstream fragment, respectively) needed to assemble the Mutagenic DNA fragment later in the protocol.

\* I use Phusion High-fidelity DNAP (NEB Cat. # M0530) for this step, but other high-fidelity enzymes such as Q5 DNAP should work as well.

1. Set up a PCR master mix for the total number of reactions needed (n) plus 10% the total number of reactions (n + n*0.1) as detailed below:

| PCR MM (25 µl) | 1 rx.   | X rx.   |
|:---------------|--------:|--------:|
| H<sub>2</sub>O | 7.5 µl  | 7.5 µl * X |
| 2X Phusion MM  | 12.5 µl | 12.5 µl * X |
| 5 ng/µl ES114 gDNA | 1 µl| 1 µl * X |
| Total =        | 21 µl   | 21 µl * X |

2. Aliquot 21 µl of PCR MM to striptubes.
3. Add 2 µl of 2.5 µM forward oligo to samples; F1 or F2-RUH.
4. Add 2 µl of 2.5 µM reverse oligo to samples; R1-LUH or R2.

\* I set up reactions using a multichannel pipette, so using 2.5 µM oligo dilutions allows me to pipette 2 µl comfortably (smaller volumes are difficult to pipette accurately with multichannel pipettes); however, a dilution of oligos at a different concentration may be used as long as you adjust the volume of oligo added and compensate with the amount of H<sub>2</sub>O in the reaction.

5. Mix and spin down samples.
6. Run reactions in thermocycler with Phusion protocol as detailed below:

| Step                 | Temperature       | Time     |
|:---------------------|------------------:|---------:|
| Initial denaturation | 98°C              | 30 sec   |
| 30 cycles:           |                   |          |
| Denaturing           | 98°C              | 5 sec    |
| Annealing            | 60°C              | 20 sec   |
| Extension            | 72°C              | 20 sec   |
| ^ back to denaturing step 29 times |     |          |
| Final extension      | 72°C              | 5 min    |
| Hold                 | 12°C              | For ever |

7. Visualize 2.5 µl of samples in a 1% Agarose gel: mix 2.5 µl reaction + 2.5 µl [6X Purple loading dye](https://www.neb.com/products/b7025-gel-loading-dye-purple-6x-no-sds#Product%20Information) (NEB) + 10 µl H<sub>2</sub>O. Load 10 µl on gel.

Example of successful reactions (ladder is [1 Kb DNA ladder](https://www.neb.com/products/n3232-1-kb-dna-ladder#Product%20Information) from NEB):

<IMG SRC="/images/sequence-tagged-gene-deletion/2018-04-02_eHB29_Homology-Arms-PCR_Example.png" WIDTH=300>
<br>
8. Purify the DNA from the successful reaction with the QIAquick PCR Purification Kit (QIAgen, Cat. No. 28106) and elute in 30 µl EB buffer.
9. Determine DNA concentration.
10. Store DNA @ -20°C.

## IV - Amplification of Barcoded Erm<sup>R</sup> Marker
In this section you will generate a DNA fragment containing an antibiotic resistance marker (in this case Erm<sup>R</sup>) flanked by FRT sites, a spacer, a barcode region, and the LUH and RUH sequences arranged as follows: LUH-FRT-Erm<sup>R</sup>-FRT-spacer-barcode-RUH.
The template used is pHB1, which carries LUH-FRT-Erm<sup>R</sup>-FRT-spacer, and the oligos used are LUH (HB42) and ErmR-RUH-BarRnd_v2 (HB154: CGATCTTGTGGGTAGAGACATCCAGGTCAAGTCnnbnnbnnbnnbnnbnnbGGAATCAAGTGCATGAGCGCTGAAG).
Oligo HB154 contains 18 semi-random basepairs that result in LUH-FRT-Erm<sup>R</sup>-FRT-spacer-barcode-RUH DNA fragments with unique sequences within the barcode region while concurrently ensuring the absence of stop codons within this sequence.
Since only one of these sequence-tagged DNA fragments will replace the target gene, this ensures that each gene deletion is tagged with a unique barcode sequence that is in-frame with the rest of the scar and lacks stop codons.
An oligo with a specific barcode sequence can be substituted for HB154 to generate the same Erm<sup>R</sup>-carrying DNA fragment with a specific sequence instead of a random one; *e.g.*, HB41 (CGATCTTGTGGGTAGAGACATCCAGGTCAAGTCcagccccgctctagtttgGGAATCAAGTGCATGAGCGCTGAAG).

1. Set up PCR as detailed below:

| PCR MM (50 µl) | 1 rx. |
|:---------------|------:|
| H<sub>2</sub>O | 22 µl |
| 2X Phusion MM  | 25 µl |
| 10 µM HB42     | 1 µl  |
| 10 µM HB154    | 1 µl  |
| 1 ng/µl pHB1   | 1 µl  |
| Total =        | 21 µl |

2. Mix and spin down samples.
3. Run reactions in thermocycler with Phusion protocol as detailed in section III above with the following modifications:
  - Annealing temperature = 60°C
  - Extension time = 20 S

4. Run whole reactions in a 1% Agarose gel.
5. Cut out 1 kb band from gel.
8. Purify DNA from the gel slices with the QIAgen Gel Extraction kit and elute in 30 µl EB.
9. Determine DNA concentration.
10. Make a 10 ng/µl ErmR-bar DNA working dilution.
11. Store DNA @ -20°C.

## V - SOE-PCR and Generation of Mutagenic DNA
In this section you will use Splicing by Overlap Extension PCR (SOE-PCR) to fuse the upstream, downstream, and Erm<sup>R</sup> Marker DNA fragments into one DNA molecule that I call Mutagenic DNA.
When inserted into VF, this Mutagenic DNA will replace the targeted gene with LUH-FRT-Erm<sup>R</sup>-FRT-spacer-barcode-RUH, generating the desired deletion.
The overall approach is to 

## VI - *tfoX* Transformation
In this section you will insert the Mutagenic DNA into VF using natural transformation.
## VII - Screening and Sequencing Δ*gene*::erm-bar Candidates

## VIII - Removal of Erm<sup>R</sup> by FLP Recombinase

## IX - Screening and Sequencing Δ*gene*::bar Candidates

## X - Adding Deletion Strains to Database
\* Barcode in notes?

## XI - Final Deletion Verification
