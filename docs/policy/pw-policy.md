# Password Politik.

??? info "Bruger password/brugernavn"
    ## Bruger password/brugernavn:
    Bruger password/brugernavn skal opbevares i vores egen self-hosted bitwarden manager. Denne 
    password manager skal kun bruges til arbejde, da den ellers har højere risiko for at blive 
    komprimeret af dette.


??? info "Sikkerheds keys eller andre sikkerhedsnoter:"
    ## Sikkerheds keys eller andre sikkerhedsnoter:
    Sikkerheds keys samt andre sikkerhedsnoter eller passwords til systemer skal også ligge i vores egen 
    self-hosted bitwarden manager, de skal dog ikke lige i brugernes ”privat” passwords, men i den 
    organisation som de er blevet tildelt.


??? info "Organisationer i bitwarden:"
    ## Organisationer i bitwarden:
    Denne organisation kan have forskellige navne alt efter hvilken afdeling brugeren er del af, så 
    sysadmins har adgang til rp-helpdesk, denne organisation giver adgang til alle vores server og 
    services på admin level, sådan at vi kan ændre og oprette på alt underliggende infrastruktur.


??? info "Backup af bitwarden:"
    ## Backup af bitwarden:
    Da det ikke er muligt for admins at tage backup af din personlige bitwarden, anbefaler vi stærkt at 
    du tager backup en gang om måned, der vil også blive opsat en mail reminder til at minde folk om at 
    få dette gjort, disse backupfiler vil blive indsamlet på et enkrypteret USB.


??? info "Backup af organisationer:"
    ## Backup af organisationer:
    Backup af organisationer bliver fortaget af admins også på en månedlig basis, det ville blive gjort på 
    samme måde som for den enkelt bruger, disse filer ville dog blive lagt på et andet enkrypteret USB
    end brugernes backup.


??? info "Bitwarden 2FA:"
    ## Bitwarden 2FA:
    Brugerne skal bruge 2FA på selve bitwarden, for at yderligere sikre password manageren. Der vil 
    blive indkøbt og uddelt Yubico YubiKey til dette formål, sådan at vi kan opnå den højeste sikkerhed 
    muligt i forhold til brute force attacks.


??? info "Send følsomme data:"
    ## Send følsomme data:
    Hvis der er behov for at sende følsomme data til andre både internt eller eksternt, så skal dette forgå 
    igennem bitwarden for at sikre data ikke bliver lækket, fordi det bliver sendt via et usikkert medie.
    Denne funktion fungerer både med eller uden password på linket som sendes til modtageren, der 
    kan også indstilles udløbsdato eller antal gang linket kan bruges.