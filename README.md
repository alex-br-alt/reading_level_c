# book_level_c
//Program in C to calculate what reading level a text is categorized as

//Background: The Coleman-Liau index is a formula where where the average number of letters per 100 words in the text, and the average number of sentences per 100 words in the text are used to decide the reading difficulty of a text. The Coleman-Liau index is: index = 0.0588 * L - 0.296 * S - 15.8


#include <ctype.h>
#include <cs50.h>
#include <math.h>
#include <stdio.h>
#include <string.h>

int count_letters(string text);
int count_words(string text);
int count_sentence(string text);

int main(void)
{
    string text = get_string("Text: ");
    
    //call the functions below
    int letters = count_letters(text);
    int words = count_words(text);
    int sentence = count_sentence(text);

    //calculate average letters per 100 words
    float L = (100 * (float)letters) / (float)words;
    float S = (100 * (float)sentence) / (float)words;

    //compute and print grade level
    float index = (0.0588 * L) - (0.296 * S) - 15.8;
    int r_index = round(index);

    if (r_index < 3)
    {
        printf("Before Grade 1\n");
    }
    else if (r_index >= 3 && r_index <= 16)
    {
        printf("Grade %d\n", r_index);
    }
    else
    {
        printf("Grade 16+\n");
    }

}

int count_letters(string text)
{
    int letters = 1;
    for (int n = 0, len = strlen(text); n < len; n++)
    {
        if (isalpha(text[n]))
        {
            letters++;
        }
    }
    return letters;
}

int count_words(string text)
{
    int words = 1;
    for (int n = 0, len = strlen(text); n < len; n++)
    {
        if (text[n] == ' ' || text[n] == '\0')
        {
            words++;
        }
    }
    return words;
}

int count_sentence(string text)
{
    int sentence = 0;
    for (int n = 0, len = strlen(text); n < len; n++)
    {
        if (text[n] == '.' || text [n] == '!' || text[n] == '?')
        {
            sentence++;
        }
    }
    return sentence;
}


//Assignment via CS50: https://pll.harvard.edu/course/cs50-introduction-computer-science?delta=0

// More information on the Coleman-Laiu Index: https://en.wikipedia.org/wiki/Coleman%E2%80%93Liau_index
