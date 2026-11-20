# Exercici 9: la mida del model (ampliació)

**Objectiu:** comparar un model petit i un de més gran amb els mateixos prompts i la mateixa configuració.

**Predicció (abans de començar):** en què creieu que es notarà més la diferència entre el model petit i el gran?

**La vostra predicció:**

1. Descarregueu la versió d'1B paràmetres (la de 4B ja la teniu de la Preparació):

   ```
   ollama pull gemma3:1b
   ```

2. **Actualitzeu `lab.py`:** afegiu l'opció `--model` (per defecte, `gemma3:4b`) i feu que, després de cada resposta, l'script imprimeixi els tokens per segon (`eval_count` dividit per `eval_duration`, que és en nanosegons: `eval_count / eval_duration * 1e9`). **Comproveu** que apareixen les dues coses i que tot l'anterior continua funcionant: `python lab.py "Hola" --vegades 1 --temperature 0 --num_predict 10 --model gemma3:1b` ha de mostrar els tokens generats, `prompt_eval_count` **i** els tokens per segon.
3. Feu els quatre prompts a cada model, amb temperatura 0. Aquest bucle de PowerShell ho fa tot d'una vegada (8 execucions):

   ```powershell
   $prompts = @(
       "Quantes lletres «r» hi ha a la paraula «strawberry»?",
       "Quantes lletres «r» hi ha a la paraula «ferrocarril»?",
       "Escriu una frase en català sobre Barcelona.",
       "Quant fa 17 × 23? Explica-ho pas a pas."
   )
   foreach ($model in "gemma3:1b", "gemma3:4b") {
       foreach ($p in $prompts) {
           python lab.py $p --vegades 1 --temperature 0 --model $model
       }
   }
   ```

4. Anoteu a la taula la resposta i la velocitat (tokens per segon) de cada model. La velocitat depèn molt de l'ordinador: sense targeta gràfica serà bastant més baixa.

| Prompt | gemma3:1b | gemma3:4b |
| :- | :- | :- |
| Lletres «r» a «strawberry» (la resposta correcta és 3) | | |
| Lletres «r» a «ferrocarril» (la resposta correcta és 4) | | |
| Frase en català (s'entén? té errors?) | | |
| 17 × 23 (la resposta correcta és 391) | | |
| Ha respost en català? | | |
| Velocitat (tokens per segon) | | |

## Preguntes

1. Quines diferències de qualitat observeu entre els dos models?

   **Resposta:**

2. I de velocitat? Quin és l'equilibri entre mida, qualitat i recursos?

   **Resposta:**

3. Per què creieu que comptar lletres és difícil per a un LLM? (Pista: el model veu tokens, no lletres.)

   **Resposta:**

