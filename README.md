# Smart-Digital-Lock-System-Using-VHDL 
entity Smart_Digital_Lock is
    Port (
        clk      : in  STD_LOGIC;
        reset    : in  STD_LOGIC;
        password : in  STD_LOGIC_VECTOR(3 downto 0);
        enter    : in  STD_LOGIC;
        unlock   : out STD_LOGIC;
        alarm    : out STD_LOGIC
    );
end Smart_Digital_Lock;

architecture Behavioral of Smart_Digital_Lock is

    constant CORRECT_PASSWORD : STD_LOGIC_VECTOR(3 downto 0) := "1010";

    signal attempts : integer range 0 to 3 := 0;

begin

process(clk, reset)

begin

    if reset = '1' then
        unlock <= '0';
        alarm <= '0';
        attempts <= 0;

    elsif rising_edge(clk) then

        if enter = '1' then

            if password = CORRECT_PASSWORD then
                unlock <= '1';
                alarm <= '0';
                attempts <= 0;

            else
                unlock <= '0';

                if attempts < 2 then
                    attempts <= attempts + 1;
                    alarm <= '0';
                else
                    alarm <= '1';
                end if;

            end if;

        end if;

    end if;

end process;

end Behavioral;