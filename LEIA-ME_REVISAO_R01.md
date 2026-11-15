# POWER BOARD SERIAL MAX3232 — Revisão R01 — 2026-11-12
Zat Electronic · KiCad 10.0 · padrão Zat (doc 11)

## CORREÇÃO DE CIRCUITO (autorizada) — buck LM2596
Antes (esquema e PCB): U2 pino 2 (OUT, chave) ligado direto no +5V/C6/J2/U3; L1 entre +5V e FB; D2 do FB para o C6–; C6– sem GND.
Agora (datasheet LM2596): U1.2 OUT -> nó SW (L1 + catodo D2); anodo D2 -> GND; L1 -> +5V (C2+, FB, J2, U2); C2– -> GND.
No PCB, sem mover componentes:
- Trilha U1.2 -> pad de cima do L1 (que já ia ao D2) = nó SW.
- Pad de baixo do L1 (já ligado ao C2+/J2/U2) = +5V.
- FB (U1.4) -> via 1,0/0,5 em (156,30; 67,46) -> B.Cu até a trilha +5V em y = 79,86.
- Trilha D2.A–C2– passou a GND (liga na zona).
Removidas: trilha FB antiga (152,79 -> 160,58) e o trecho L1(baixo) -> pad.

## Outras alterações de cobre (autorizadas)
- C5 (novo) 100nF 0805: desacoplamento do VCC do MAX3232 (U3 pino 16), em (169,805; 93,6) -90°, trilha 0,5 mm até a malha +3,3V.
- 3 vias com anel 0 (1,0/1,0): furo 0,5 mm, diâmetro 1,0 mantido.
- Trilha +24V duplicada com ponta solta no J1 removida (não muda a ligação).
- Zona GND sem preenchimento salvo (o cobre mudou): preencher com B. Simulação: todo o GND fica num só grupo.

## Esquema
- Esquema plano -> capa A2 + 2 folhas: 02 ALIMENTAÇÃO (A3), 03 SERIAL (A4).
- Reanotação (todo o esquema): U2->U1 (LM2596), U3->U2 (AMS1117), U1->U3 (MAX3232);
  C5->C1, C6->C2, C7->C3, C1->C4, C8(novo)->C5, C2->C6, C3->C7, C4->C8. J/D/F/L/H iguais.
- D1/D2: Device:D_Schottky (SS54 não existe na biblioteca KiCad), Value SS54.
- J1/J2: ZAT_Connector:Screw_Terminal_01x02 + ZAT_TerminalBlock:TerminalBlock_MaiXu_MX126-5.0-02P_1x02_P5.00mm_DG306
  (3D ${ZAT_3D}/BORNE KRE VARIOS/DG306-5.0-02P-12-00AH.STEP). O footprint AK300-2 não existe no KiCad 10.
  Pinos 1/2 trocados para a entrada do fio ficar para fora da placa: J1 pino 1 = +24V, J2 pino 1 = +5V.
  Furos nas mesmas posições.
- Valores normalizados (100nF/50V, 680uF/16V, 33uH...), Descrição PT, Stock Code, Package Group.
- PWR_FLAG no nó VIN (depois do D1), em GND e em +5V. Nenhuma severidade em "ignore".

## PCB (fora o cobre acima, nada mudou)
- Footprints atualizados para a biblioteca KiCad 10: C 0805, F1 2010, J3 2x08, U3 SOIC-16, U1 TO-263-5. O 3D passa a ser o padrão do KiCad.
- Logos: courtyard real + "Not in schematic". Os 4 logos de canto foram afastados 1,0-1,4 mm dos furos M3 (o courtyard encostava no do furo).
- Arte de serigrafia em volta do J3: 3 bordas recuadas 0,2 mm (silk_overlap com o contorno do J3).
- Referências visíveis em F.SilkS 1,0 mm. .kicad_dru só com "(version 1)".

## Biblioteca global (já gravada no PC)
- symbols/ZAT_Connector: + Screw_Terminal_01x02
- footprints/ZAT_TerminalBlock: + TerminalBlock_MaiXu_MX126-5.0-02P_1x02_P5.00mm_DG306

## Pontos de projeto
- IMPORTANTE: entrada 24 V com C1 de 35 V (margem de 46%); considere 50 V se a fonte tiver picos.
- ATENÇÃO: se esta placa já foi montada com o circuito antigo, o buck não funcionava como regulador (saída chaveada direto na carga).
- MELHORIA: o laço de corrente do buck (U1.2 -> D2 -> GND) ficou com ~13 mm de trilha; no próximo layout, aproximar D2 do U1 e C1.
- MELHORIA: a entrada do AMS1117 (U2) usa o C2 680 uF do buck como capacitor de entrada (longe); um 10 uF perto do U2 é recomendado.
- MELHORIA: o packages3D antigo (AK300/1808/.wrl) não é mais usado pelos footprints; ficou só como cópia.

## Após abrir no KiCad
1. Reiniciar o KiCad (bibliotecas atualizadas).
2. ERC no esquema.
3. PCB: B (preencher zonas) -> F8 (deve vir sem alterações) -> DRC.
