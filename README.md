package me.TrickyPvP.Network.Kits.Kits;

import me.TrickyPvP.Network.API.KitAPI.KitApi;
import me.TrickyPvP.Network.Kits.KitManager.KitManager;
import me.TrickyPvP.Network.Listeners.NoMove;
import me.TrickyPvP.Network.Main.Main;

import org.bukkit.Bukkit;
import org.bukkit.ChatColor;
import org.bukkit.Location;
import org.bukkit.Material;
import org.bukkit.entity.Player;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.player.PlayerInteractEntityEvent;

public class Gladiator implements Listener{
	
	Location loc = new Location(Bukkit.getWorld("hub"), 6, 77, 9);
	
	Main pl = Main.getInstance();
	
	public Gladiator(Main pl){
		this.pl = pl;
	}
	
	@EventHandler
	public void onPlayerRightClick(PlayerInteractEntityEvent e){
		Player clicked = (Player) e.getRightClicked();
		Player clicker = e.getPlayer();
		if(e.getRightClicked() instanceof Player){
			System.out.print("DEBUG 1");
			
			if(KitManager.Gladiator.contains(clicker.getName()) && clicker.getItemInHand().equals(Material.IRON_INGOT)){
				KitApi.tpPlayers(clicker, clicked);
				System.out.print("DEBUG 2");
			}
		}
		NoMove.NoMove.add(clicked.getName());
		NoMove.NoMove.add(clicker.getName());
		Bukkit.getScheduler().runTaskLater(pl, new Runnable() {
			public void run(){
				clicker.sendMessage(ChatColor.RED + "3...");
				clicked.sendMessage(ChatColor.RED + "3...");
				System.out.print("DEBUG 3");
				Bukkit.getScheduler().runTaskLater(pl, new Runnable() {
					public void run(){
						clicker.sendMessage(ChatColor.RED + "2...");
						clicked.sendMessage(ChatColor.RED + "2...");
						System.out.print("DEBUG 4");
						
						Bukkit.getScheduler().runTaskLater(pl, new Runnable() {
							public void run(){
								clicker.sendMessage(ChatColor.YELLOW + "1...");
								clicked.sendMessage(ChatColor.YELLOW + "1...");
								System.out.print("DEBUG 5");
								Bukkit.getScheduler().runTaskLater(pl, new Runnable() {
									public void run(){
										clicker.sendMessage(ChatColor.GREEN + "VAI!");
										clicked.sendMessage(ChatColor.GREEN + "VAI!");
										System.out.print("DEBUG 6");
										NoMove.NoMove.remove(clicker.getName());
										NoMove.NoMove.remove(clicked.getName());
			}
			
			
		}, 20);
		
	}

}, 20);
					}
				}, 20);
			}
		}, 20);
		
		if(clicker.getHealth() == 0){
			System.out.print("DEBUG 7");
			clicked.sendMessage(ChatColor.GREEN + "Tu Ganhaste!");
			clicker.sendMessage(ChatColor.RED + "Tu Perdeste!");
			clicker.teleport(loc);
			clicked.teleport(loc);
		}else if(clicked.getHealth() == 0){
			System.out.print("DEBUG 8");
			clicker.sendMessage(ChatColor.GREEN + "Tu Ganhaste!");
			clicked.sendMessage(ChatColor.RED + "Tu Perdeste!");
			clicker.teleport(loc);
			clicked.teleport(loc);
		}else{
			System.out.print("DEBUG 9");
			
			return;
		}
		

	}
	
}
