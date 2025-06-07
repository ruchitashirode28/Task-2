# Task-2
#include <stdio.h>
#include <ctype.h>

void analyzeFile(const char *filename);

int main() {
    char filename[100];

    printf("Enter the filename to analyze: ");
    scanf("%s", filename);

    analyzeFile(filename);

    return 0;
}

void analyzeFile(const char *filename) {
    FILE *file = fopen(filename, "r");

    if (file == NULL) {
        printf("Error: Could not open file '%s'\n", filename);
        return;
    }

    int lines = 0, words = 0, characters = 0;
    char ch;
    int inWord = 0;

    while ((ch = fgetc(file)) != EOF) {
        characters++;

        if (ch == '\n') {
            lines++;
        }

        if (isspace(ch)) {
            inWord = 0;
        } else if (!inWord) {
            inWord = 1;
            words++;
        }
    }

    // If the last line doesn't end with a newline
    if (characters > 0 && ch != '\n') {
        lines++;
    }

    fclose(file);

    printf("\n--- File Analysis ---\n");
    printf("File: %s\n", filename);
    printf("Lines     : %d\n", lines);
    printf("Words     : %d\n", words);
    printf("Characters: %d\n", characters);
}
