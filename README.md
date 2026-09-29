from deep_translator import GoogleTranslator

def translate_text(text, dest_lang):
    try:
        translated_text = GoogleTranslator(source='auto', target=dest_lang).translate(text)
        return translated_text
    except Exception as e:
        return f"Error: {type(e).__name__}: {e}"

def main():
    supported_langs_raw = GoogleTranslator().get_supported_languages(as_dict=True)
    supported_langs = {v: k for k, v in supported_langs_raw.items()}

    print("Available languages:")
    print(", ".join(f"{code}: {name}" for code, name in sorted(supported_langs.items())))

    text = input("\nText to translate: ").strip()
    if not text:
        print("No text entered.")
        return

    dest_lang = input("Destination language code: ").strip().lower()

    if dest_lang not in supported_langs:
        print(f"Invalid language code: '{dest_lang}'")
        return

    print(f"\nOriginal  : {text}")
    print(f"Translated: {translate_text(text, dest_lang)}")

if __name__ == "__main__":
    main()
