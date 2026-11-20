# Exercici 10: sortida estructurada en JSON (ampliació)

**Objectiu:** obtenir respostes que un programa pugui llegir. Quan un LLM forma part d'una aplicació, la resposta sovint ha de ser JSON vàlid, no text lliure.

**Predicció (abans de començar):** si demaneu al model que respongui en JSON, la resposta es podrà llegir directament amb `json.loads`?

**La vostra predicció:**

1. **Actualitzeu `lab.py`:** afegiu l'opció `--format json`. Atenció: `format` **no** va dins d'`options`, sinó com a argument directe de `ollama.generate`. Feu també que, després de cada resposta, l'script indiqui si és JSON vàlid (provant `json.loads`). **Comproveu** que ho indica i que continuen sortint els tokens generats i `prompt_eval_count`: `python lab.py "Hola" --vegades 1 --temperature 0 --num_predict 10 --format json`.
2. Deseu aquest prompt en una variable de PowerShell:

   ```powershell
   $prompt = "Extreu les dades d'aquesta frase: «La Marta té 34 anys, viu a Girona i treballa de programadora.» Respon en JSON amb les claus nom, edat, ciutat i ofici."
   ```

3. Executeu-lo amb temperatura 0, primer sense `--format` i després amb `--format json`, i compareu les dues respostes:

   ```powershell
   python lab.py $prompt --vegades 1 --temperature 0
   python lab.py $prompt --vegades 1 --temperature 0 --format json
   ```

4. Repetiu les dues ordres amb `--temperature 1.5`. La resposta amb `--format json` continua sent JSON vàlid?

## Preguntes

1. Per què falla `json.loads` amb la primera resposta, si el contingut sembla correcte?

   **Resposta:**

2. Què fa el paràmetre `format="json"`? Garanteix que les dades siguin correctes o només que el format sigui vàlid?

   **Resposta:**

3. En quin tipus d'aplicació necessitaríeu que el model respongués sempre en JSON?

   **Resposta:**

