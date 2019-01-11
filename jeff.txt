from discord.ext import commands
import discord

client = commands.Bot(command_prefix ='.')

@client.event
async def on_ready():
    await client.change_presence(game=discord.Game(name='Working on discord server!'))
    print('Bot is ready.')



@client.event
async def on_member_join(member):
    await Client.send_message(Client.get_channel('ROOM ID'), ('Welcome ' + member.mention))
#This is Welcome

    
@client.event
async def on_member_join(member):
    role=discord.utils.get(member.server.roles, name='ROLE ON THE SERVER')
    await client.add_roles(member, role)
#This is Autorole
 




@client.command(pass_context = True)
async def clear(ctx, number):
    mgs = [] 
    number = int(number)
    async for x in client.logs_from(ctx.message.channel, limit = number):
        mgs.append(x)
    await client.delete_messages(mgs)
#This is clear messages







@client.command(pass_context = True)
async def ban(member: discord.Member):
    await client.ban(user.mention)
#This is ban message#







@client.command()
async def commands():
    await client.say("""```css
Commands - All of the commands.
Clear - Clear messages.
Ban - Ban's the mentioned user.
Kick - Kick's the mentioned user.
For more info about this commands do:
.I(Name of the command)
Example: .Icommands```""")
#commands message

    
@client.command()
async def Iclear():
    await client.say("""```css
Clear - The command clears the messages by using .clear (amount)
The amount has to be between 2 and 100.```""")
#info of clear






@client.command()
async def Iban():
    await client.say("""```css
Ban - The command bans the mentioned user.```""")
#info of ban





@client.command()
async def Ikick():
    await client.say("""```css
Kick - The command kicks the mentioned user.```""")
#info of kick
    
    
@client.command()
async def Icommands():
    await client.say("""```css
Commands - This command gives you a list with helpful commands.```""")
#info of commands







players = {}
@client.command(pass_context=True)
async def join(ctx):
    channel = ctx.message.author.voice.voice_channel
    await client.join_voice_channel(channel)

@client.command(pass_context=True)
async def leave(ctx):
    server = ctx.message.server
    voice_client = client.voice_client_in(server)
    await voice_client.disconnect()

@client.command(pass_context=True)
async def play(ctx, url):
    server = ctx.message.server
    voice_client = client.voice_client_in(server)
    player = await voice_client.create_ytdl_player(url)
    players[server.id] = player
    player.start()





@client.command(pass_context=True)
async def pause(ctx):
    id = ctx.message.server.id
    players[id].pause()






@client.command(pass_context=True)
async def stop(ctx):
    id = ctx.message.server.id
    players[id].stop()





@client.command(pass_context=True)
async def resume(ctx):
    id = ctx.message.server.id
    players[id].resume()





client.run('NTMzMjgzMjMxMjE1MjU1NTUy.DxoykQ.P-YSmFZXgVeZ22sYzGVkeqD_bmQ')
