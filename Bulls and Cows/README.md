You are playing the Bulls and Cows game with your friend.

You write down a secret number and ask your friend to guess what the number is. When your friend makes a guess, you provide a hint with the following info:

The number of "bulls", which are digits in the guess that are in the correct position.
The number of "cows", which are digits in the guess that are in your secret number but are located in the wrong position. Specifically, the non-bull digits in the guess that could be rearranged such that they become bulls.
Given the secret number secret and your friend's guess guess, return the hint for your friend's guess.

The hint should be formatted as "xAyB", where x is the number of bulls and y is the number of cows. Note that both secret and guess may contain duplicate digits.

char * getHint(char * secret, char * guess){
    int count[10] = {0};
    int i = 0, len = strlen(secret);
    int bulls = 0, cows = 0;
    char *ret = NULL;
    unsigned int bulldigits = 1, cowdigits = 1, outlen = 0;

    for (i = 0; i < len; i++) {
        int digit = secret[i] - '0';
        count[digit]++;
    }
    for (i = 0; i < len; i++) {
        int digit = guess[i] - '0';
        if (guess[i] == secret[i]) {
            bulls++;
            count[digit]--;
        } 
    }
    for (i = 0; i < len; i++) {
        int digit = guess[i] - '0';
        if (guess[i] != secret[i]) {
            if (count[digit] > 0) {
                cows++;
                count[digit]--;
            }
        }
    }

    if (bulls != 0) {
        bulldigits = (unsigned int) ((log10((double) bulls)) + 1);
    }
    
    if (cows != 0) {
        cowdigits = (unsigned int) ((log10((double) cows)) + 1);
    }
    
    outlen = bulldigits + cowdigits + 3;
    ret = (char *) malloc (outlen * sizeof(char));
    
    snprintf(ret, outlen, "%dA%dB", bulls, cows);
    
    return ret;
}
