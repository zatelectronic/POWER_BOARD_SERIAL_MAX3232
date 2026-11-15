# POWER BOARD SERIAL MAX3232 — Revisão R02 — 2026-11-12
Zat Electronic · KiCad 10.0 · base: arquivos editados pelo Kenneth (trilhas e textos dele mantidos)

## ERC (2 erros -> 0)
- four_way_junction (folha 02, nó VIN): o PWR_FLAG do VIN saía da junção D1/C1/U1 (4 fios).
  Agora o flag sai do fio D1 -> junção, 2,54 mm antes. Nó continua o mesmo.
- power_pin_not_driven (+24V): a rede +24V só tinha J1 e F1 (passivos).
  PWR_FLAG + símbolo +24V incluídos no quadro "ERC POWER FLAGS".

## 3D que faltava (footprints ZAT novos)
Cópias exatas do KiCad 10 com o 3D da pasta ${ZAT_3D}:
- F1: ZAT_Fuse:Fuse_2010_5025Metric_Pad1.52x2.65mm_HandSolder_1808-2410
  (3D: ${ZAT_3D}/FUSES/1808-2410 贴片保险丝.STEP).
- L1: ZAT_Inductor_SMD:L_12x12mm_H8mm_33uH
  (3D: ${ZAT_3D}/INDUTOR/L_12x12mm_H8mm.step).
- Pads e serigrafia iguais aos do KiCad. Posição, rotação e trilhas não mudaram.

## Biblioteca global (já gravada no PC)
- footprints/ZAT_Fuse.pretty (nova) e footprints/ZAT_Inductor_SMD.pretty (nova).
- fp-lib-table: + ZAT_Fuse, + ZAT_Inductor_SMD.

## Após abrir no KiCad
1. Reiniciar o KiCad (tabela de bibliotecas atualizada).
2. ERC no esquema.
3. PCB: B (preencher zonas) -> F8 (deve vir sem alterações) -> DRC.
