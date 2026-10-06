# Supply Chain Lab - Revisão de Dependências

Exercício prático **sem nota** sobre **segurança da cadeia de suprimentos de software**.
Você é a pessoa de segurança do time da OrbitaPay (empresa **fictícia**). Um bot abriu PRs de atualização de dependências e um colega propôs um pacote novo. Para cada PR, você decide: **aceitar, aceitar com condições, rejeitar ou investigar**, citando o que verificaria (SBOM, assinatura/provenance, CVE, lockfile...).

> Todos os pacotes, mantenedores e domínios são **fictícios**. O código mostrado é ilustrativo e **não executa nada**.
> Nunca execute pacotes de origem desconhecida na sua máquina para "ver o que acontece".

## Como abrir
1. Baixe a pasta e dê **duplo clique em `index.html`** (qualquer navegador atual). Não precisa de internet nem instalação.
2. Se quiser, digite seu nome/RM no topo (só aparece no relatório que você baixar).

## O que fazer (sugestão: 40-60 min, 7 PRs)

Em cada PR:
1. Leia o **changelog** e os **metadados do registro**.
2. **Execute as verificações** que achar necessárias (auditoria, histórico de mantenedores, provenance, diff do SBOM, hash do lockfile, scripts de instalação, diff do código). Cada uma revela evidências.
3. Escolha o **veredito**:
   - **Aceitar**: seguro e útil, siga o fluxo normal;
   - **Aceitar com condições**: legítimo, mas exige testes, revisão ou aprovação antes;
   - **Rejeitar**: não deve entrar;
   - **Investigar antes de decidir**: há indício forte; bloqueie por ora e apure.
4. Marque os **sinais de risco** que viu (e os **sinais a favor**) e as **ações** que tomaria.
5. Escreva a justificativa e clique em **Registrar revisão**. Aparece a análise de referência.

Botões do topo: **Relatório** (baixa um `.md`), **Debrief** (checklist e perguntas de discussão) e **Reiniciar**.

## Conceitos para consultar
| Termo | O que é |
|---|---|
| **SBOM** | Software Bill of Materials: lista de todos os componentes (e versões) do seu software. |
| **Provenance / assinatura** | Prova criptográfica de que o pacote foi construído a partir de determinado repositório/CI. |
| **Lockfile** | Arquivo que trava as versões e os hashes exatos instalados (ex.: `package-lock.json`). |
| **Integrity (hash)** | Garante que o arquivo é o publicado, mas **não** que ele é seguro. |
| **Typosquatting** | Pacote malicioso com nome quase igual ao de um popular. |
| **Dependency confusion** | Pacote público com o mesmo nome de um pacote interno, para o gerenciador instalar a versão errada. |
| **CVE** | Identificador de vulnerabilidade **conhecida**. Backdoors novos não têm CVE. |
| **Cooldown** | Esperar alguns dias antes de adotar uma versão recém-publicada. |

## Dicas (sem spoilers)
- **Nem todo PR é perigoso.** Rejeitar tudo por precaução também custa caro (correções de segurança não entram).
- **Confira se o changelog e o diff contam a mesma história.**
- **Quem publicou?** Mudanças recentes de mantenedor merecem atenção.
- **Assinatura/provenance:** as versões anteriores tinham? Esta tem?
- **Leia o diff do lockfile**, não só o do código: tudo que muda lá entra na sua aplicação.
- **Scripts de instalação** (`preinstall`/`postinstall`) rodam na máquina de quem instala: na sua e no CI.
- **"Hash OK" não significa "seguro".** Pergunte: OK em relação a quê?
- **Ausência de CVE não é prova de segurança**, principalmente para versões novas.
- **Nome parecido? Pacote novo? Quase sem downloads?** Desconfie, mas lembre que quem sugeriu pode estar de boa-fé.
- **Pense na ação, não só no veredito:** o que fazer com o PR, com o colega, com o CI e com os segredos.

## Combinados
- Ambiente de **treino**: errar faz parte.
- Discuta com a dupla, mas **registre a sua própria revisão**.
- Não compartilhe a análise de referência com quem ainda não terminou.
