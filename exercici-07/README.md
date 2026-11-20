# Exercici 7: num_ctx, la memòria del model

**Objectiu:** comprovar que el model només «recorda» el que cap dins la finestra de context.

El **context** (`num_ctx`) és la «memòria de treball» del model: el nombre màxim de tokens que pot tenir en compte alhora. Si el text és més llarg que el context, el model no el pot tenir tot a la vista.

**Predicció (abans de començar):** si el text és més llarg que el context, quina part creieu que oblidarà el model: el principi o el final?

**La vostra predicció:**

## Preparar els textos

1. A la carpeta `exercici-07/` hi ha l'ajudant `genera_text.py`, que genera un text llarg de la mida (en tokens) que li demaneu: comença amb la frase de `--inici` (el secret), continua amb frases de farciment i acaba amb la de `--final` (la pregunta). Només fa servir Ollama per comptar tokens: **no li fa cap pregunta**. No cal que el llegiu a fons.
2. Genereu dos textos de mides diferents, des de l'arrel del repositori i amb l'entorn virtual activat. Es creen `text_1000.txt` i `text_6000.txt`, amb el secret al principi i la pregunta al final, i l'ajudant us diu quants tokens té exactament cadascun:

   ```powershell
   $inici = "El codi secret és PASSWORD-1234. Recorda'l."
   $final = "Pregunta: quin era el codi secret? Respon en una sola frase."
   python exercici-07/genera_text.py 1000 --inici $inici --final $final
   python exercici-07/genera_text.py 6000 --inici $inici --final $final
   ```

## Actualitzar l'script

3. **Actualitzeu `lab.py`:** demaneu al model que hi afegeixi:
   - l'opció `--num_ctx` (mida del context), que va dins d'`options`;
   - l'opció `--fitxer`, que llegeix el prompt d'un fitxer de text en lloc de la línia d'ordres (si s'indica, el prompt de la línia d'ordres ja no és obligatori);
   - la impressió, després de cada resposta, del valor `prompt_eval_count` de la resposta d'Ollama.

   *Pista:* perquè el prompt de la línia d'ordres sigui opcional, digueu-li que a `argparse` ha de ser un argument amb `nargs="?"`.

   **Comproveu el resultat:** després de cada resposta ha de sortir `prompt_eval_count` (si no hi és, demaneu-li al model que l'afegeixi) i les opcions anteriors han de continuar funcionant: `python lab.py "Hola" --vegades 1 --temperature 0 --num_predict 10 --num_ctx 2048` ha de mostrar els tokens generats **i** `prompt_eval_count`. Amb `--fitxer` i `num_ctx` 8192, el `prompt_eval_count` ha de coincidir amb els tokens que ha dit `genera_text.py`; si és més gran (per exemple, 1112 en lloc de 1003), el fitxer no es llegeix en UTF-8 i cal demanar al model que l'obri amb `encoding="utf-8"`.

## Fer les proves

4. Feu la pregunta al model amb cada text i cada context. Per exemple, per al text de 6000 tokens i el context de 2048:

   ```powershell
   python lab.py --fitxer text_6000.txt --vegades 1 --temperature 0 --num_predict 40 --num_ctx 2048
   ```

   A cada casella de la taula anoteu el valor de `prompt_eval_count` (els tokens del prompt que el model ha processat realment) i si el model recorda el codi (sí o no):

| Mida del text | `num_ctx` 2048 | `num_ctx` 8192 |
| :- | :- | :- |
| 1000 tokens | | |
| 6000 tokens | | |

Un context més gran gasta més memòria RAM. Si l'ordinador va just, genereu un text de 3000 tokens i proveu `num_ctx` 2048 i 4096 en lloc de 8192. Atenció: Ollama no accepta contextos inferiors a 2048 tokens (si demaneu 512, el puja a 2048). Podeu comprovar el context real amb `ollama ps` en un altre terminal (columna `CONTEXT`).

## Preguntes

1. Mireu la taula. Amb quines combinacions de mida del text i `num_ctx` recorda el codi el model i amb quines no? Quina relació hi ha entre la mida del text i `num_ctx`?

   **Resposta:**

2. Per què el model «omet» el principi del text quan aquest és més llarg que el context?

   **Resposta:**

3. Quin problema pràctic us podeu trobar si feu servir un model local per resumir documents llargs?

   **Resposta:**

4. Si amb 2048 el model ha respost una cosa inventada o ha negat que hi hagi cap codi: per què és perillós que ho digui amb seguretat, en lloc de dir que no ho sap?

   **Resposta:**

