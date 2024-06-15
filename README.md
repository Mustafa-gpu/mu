dependencies {
  compile group: 'org.bukkit', name: 'bukkit', version: '1.7.9-R0.1-SNAPSHOT'
  compile('io.ibj:MattLib:1.1-SNAPSHOT') {
    exclude group: 'de.bananaco'
    exclude 'net.milkbowl:vault:1.2.27'
  }
  compile group: 'net.citizensnpcs', name: 'citizens', version: '2.0.12'
  compile group: 'com.sk89q', name: 'worldedit', version: '5.6.1'
  compile group: 'com.sk89q', name: 'worldguard', version: '5.9'
  compile group: 'net.milkbowl', name: 'vault', version: '1.2.12'
  compile fileTree(dir: 'libs', includes: ['*.jar'])
}
